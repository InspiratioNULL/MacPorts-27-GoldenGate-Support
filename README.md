# MacPorts-27-GoldenGate-Support
Incase anyone wants to continue to use  MacPorts while using the developer beta macOS 27 golden gate.
```
git clone https://github.com/InspiratioNULL/MacPorts-27-GoldenGate-Support
cd MacPorts-27*
export MTCL=/opt/local/libexec/macports/lib/macports1.0/macports.tcl
sudo mv $MTCL $MTCL.bak && sudo mv macports.tcl $MTCL 
export MCONF=/opt/local/etc/macports/macports.conf 
sudo $MCONF $MCONF.bak && sudo mv macports.conf $MCONF
```
## Changes made.
 #### in ***``` /opt/local/libexec/macports/lib/macports1.0/macports.tcl ```***
  #### change line 65
 
  ``` default_compilers pkg_post_unarchive_deletions ui_interactive] {     ```
  
  **to** 
  
  
  ``` default_compilers pkg_post_unarchive_deletions ui_interactive ports_os_major] { ```
  
  **and add lines(starting at line 1196)**
  
 ```
      # Override OS version if ports_os_major is specified in macports.conf                                                                                    
      if {[info exists macports::ports_os_major]} {                                                                                                            
          set os_major $macports::ports_os_major                                                                                                               
          set macports::autoconf::os_major $macports::ports_os_major                                                                                           
          set os_version "${os_major}.0.0"                                                                                                                     
      }                                                                                                                                                        
```

#### then in  ***/opt/local/etc/macports/macports.conf***:
#### add at the end
```                                                                                                                                                             
 # Temporary override for macOS Beta to fallback to the previous Darwin version.                                                                              
  ports_os_major          26                                                                                                                                   
```
This instructs macports to use macOS 26 Tahoe as the fallback for macOS 27 during this developer beta stage where macports doesnt yet support it. This is experimental, but in my experience with it so far it has no issues, and is a lot better tahn just silently stalling and not finishing any command. when macports adds support we can comment that las tline in macports.conf out and the behavior returns to the original 
