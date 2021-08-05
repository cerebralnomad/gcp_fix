# gcp_fix
Code change to the gcp utility to eliminate deprecation warnings

Beginning with Ubuntu 20.04, gcp began throwing deprecation warnings when run.
I made a handful of changes to the code to eliminate these warnings.

The file gcp is located at /usr/share/gcp/
It can be replaced or edited using sudo privledges.

Both the original and edited versions are included in this repo for reference 
and my own use in the future until official corrections can be made upstream.

## List of changes made

Line 39, replaced

    from gi.repository import GObject
    
with:

    from gi.repository import GLib
    
Line 42, replaced

    import dbus.glib
    
with:

    from dbus.mainloop.glib import DBusGMainLoop
    
Added the following as line 43:

    DBusGMainLoop(set_as_default=True)
    
Lines 364-366 changed 

    GObject.io_add_watch(source_fd, GObject.IO_IN,self._copyFile,
                             (dest_fd, options),
                             priority=GObject.PRIORITY_DEFAULT)
                             
to:

    GLib.io_add_watch(source_fd, GLib.IO_IN,self._copyFile,
                             (dest_fd, options),
                             priority=GLib.PRIORITY_DEFAULT)
                             

Changed line 726 from 

    GObject.idle_add(self.__copyNextFile)
    
to:

    GLib.idle_add(self.__copyNextFile)
    
Changed line 736 from

    self.loop = GObject.MainLoop()
    
to:

    self.loop = GLib.MainLoop()
