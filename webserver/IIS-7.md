= Downloading and configuring the H264 Streaming Module for Internet Information
Services IIS 7 =

[http://h264.code-shop.com/trac/wiki/ back][[PageOutline]]

----

== Download ==

Download the
[http://h264.code-shop.com/download/iis7_mod_h264_streaming-2.2.7.zip
H264-Streaming-Module for IIS 7].

== Configuration IIS 7 (Windows Vista) ==

By default, IIS 7.0 is not installed on Windows Vista. You can install IIS by
clicking Windows Features in Advanced Options under Programs in Control Panel. 

When running Windows 32 bit: 

  - Create an App_Code folder, if you don't already have one, in
    c:\inetpub\wwwroot.
  - Copy the Mod-H264-Streaming module (mod_h264_streaming.dll) into this
    directory (c:\inetpub\wwwroot\app_code).

When running Windows 64 bit: 

  - Enable 32 bit applications on win 64. See:
    [http://blogs.msdn.com/rakkimk/archive/2007/11/03/iis7-running-32-bit-and-64-bit-asp-net-versions-at-the-same-time-on-different-worker-processes.aspx
IIS7 - Running 32-bit and 64-bit ASP.NET versions at the same time on different
worker processes].
  - Copy the Mod-H264-Streaming module (mod_h264_streaming.dll) into either
    (%windir%\syswow64\inetsrv) or (%windir%\system32\inetsrv) depending on your
windows version.

Open up IIS Manager.

  - Select 'MIME types'.
  - Select 'Add'.
  - Set 'File name extension' to '.mp4' and 'MIME type' to 'video/mp4'.
  - Click 'OK'.

  - Select 'Modules'.
  - Select 'Configure Native Modules'.
  - Select 'Register'.
  - Set 'Name' to 'ModH264Streaming'.
  - Set 'Path' to the path where the mod_h264_streaming.dll is located.
  - Click 'OK'.
  - Click 'OK' again.

  - Select Handler Mappings.
  - Select 'Add Module Mapping'.
  - Set 'Request Path' to '*.mp4'.
  - Set 'Module' to 'ModH264Streaming'.
  - Set 'Name' to 'ModH264Streaming'.
  - Click 'Request Restrictions'.
  - Set 'Mappings' to 'Invoke handler only if request is mapped to file'.
  - Set 'Verbs' to 'All verbs'.
  - Set 'Access' to 'Scripts'. (Note to self: verify why this was previously
    'Execute').
  - Click 'OK'.
  - Click 'OK' again.

The module now appears under the 'Enabled' Handler Mappings.

== Testing ==

Continue to the [wiki:Mod-H264-Streaming-Testing-Version2 testing] page to
verify your setup.

