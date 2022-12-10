# Downloading and configuring the H264 Streaming Module for Internet Information Services IIS =

## Download

Download the
[http://h264.code-shop.com/download/iis5_mod_h264_streaming-2.2.7.zip
H264-Streaming-Module ISAPI extension for IIS].

## Configuration IIS 5.1 (Windows XP)

In the root of the website (c:\inetpub\wwwroot).

  - Create an App_Code folder if you don't already have one.
  - Copy the Mod-H264-Streaming module (mod_h264_streaming.dll) into this
    directory (c:\inetpub\wwwroot\app_code).

Open up IIS Manager. In the site properties, click the "Home directory" tab then
click the "Configuration" button. We're going to add an entry for files ending
in .mp4

  - Click the 'Add' button.
  - Click the 'Browse' button and select the mod_h264_streaming.dll executable.
  - Place the text '.mp4' in the Extension box.
  - Set Verbs to "Limit to:" with the value GET,HEAD,POST,DEBUG.
  - Click OK

## Configuration IIS 6 (Windows Server 2003)

When running Windows 32 bit:

In the root of the website (c:\inetpub\wwwroot).

  - Create an App_Code folder if you don't already have one.
  - Copy the Mod-H264-Streaming module (mod_h264_streaming.dll) into this
    directory (c:\inetpub\wwwroot\app_code).

When running Windows 64 bit:

  - Read
    [http://www.microsoft.com/technet/prodtechnol/WindowsServer2003/Library/IIS/405f5bb5-87a3-43d2-8138-54b75db73aa1.mspx?mfr=true
Configuring IIS to Run 32-bit Applications on 64-bit Windows (IIS 6.0)] and
follow the given instructions.
  - Copy the Mod-H264-Streaming module (mod_h264_streaming.dll) into this
    directory (%windir%\syswow64\inetsrv).

Open up IIS Manager. In the site properties, click the "Home directory" tab then
click the "Configuration" button. We're going to add an entry for files ending
in .mp4

  - Click the 'Add' button.
  - Click the 'Browse' button and select the mod_h264_streaming.dll executable.
  - Place the text '.mp4' in the Extension box.
  - Set Verbs to "Limit to:" with the value GET,HEAD,POST,DEBUG.
  - Click OK

  - Click the 'Web Service Extensions'.
  - Click 'Add a new Web Service Extension'.
  - Place the text 'ModH264Streaming' in the 'Extension name' box.
  - Click 'Add' and select the mod_h264_streaming.dll executable.
  - Tick the 'Set extension status to Allowed'.

## Testing

Continue to the [testing](/wiki:Mod-H264-Streaming-Testing-Version2/) page to
verify your setup.

