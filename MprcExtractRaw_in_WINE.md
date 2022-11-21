MprcExtractRaw in Docker wine
=============================

On macOS, make sure xQuartz is installed. Then, to allow Wine to create Windows GUI elements, make sure you run the following command to allow X11 forwarding locally:

```bash
xhost + 127.0.0.1
```

```bash
docker build -t winedotnet .
```

```bash
docker run -it -v ${HOME}/mprc:/data -v ${HOME}/mprcsoft:/mprcsoft -v /private/tmp:/private/tmp -e DISPLAY=host.docker.internal:0 winedotnet bash
```

```bash
docker run -it --name rawdump -v ${HOME}/mprc:/data -v ${HOME}/mprcsoft:/mprcsoft -v ${HOME}/mprcsoft/drivec:/wineprefix64/drive_c -v /private/tmp:/private/tmp -e DISPLAY=host.docker.internal:0 winedotnet bash
```

```bash
wine64 /mprcsoft/MSFileReader-2.2.62/MSFileReader.exe
```

```bash
wine64 /mprcsoft/rawExtract/0.6/MprcExtractRaw.exe --params /data/test_wine.params
```

```bash
mkdir -p /wineprefix64/drive_c/temp && cp -f /data/msf_answers.iss /wineprefix64/drive_c/temp/
wine64 /mprcsoft/MSFileReader-2.2.62/MSFileReader.exe /s /f1"c:\temp\msf_answers.iss" /f2"c:\temp\msf_log.log" /SMS
```

```
vcredist_x64_VS2008.exe /install /quiet /norestart
vcredist_x64_VS2010.exe /install /quiet /norestart
vcredist_x86_VS2008.exe /install /quiet /norestart
vcredist_x86_VS2010.exe /install /quiet /norestart

wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x64_VS2008.exe /install /quiet /norestart
wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x64_VS2010.exe /install /quiet /norestart
wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x86_VS2008.exe /install /quiet /norestart
wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x86_VS2010.exe /install /quiet /norestart

wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x64_VS2008.exe /q
wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x64_VS2010.exe /q /norestart
wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x86_VS2008.exe /q
wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x86_VS2010.exe /q /norestart

```

```bash
mkdir -p /wineprefix64/drive_c/temp
cp -f /data/msf_answers.iss /wineprefix64/drive_c/temp/
wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x64_VS2008.exe /q
wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x64_VS2010.exe /q /norestart
wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x86_VS2008.exe /q
wine64 /mprcsoft/MSFileReader-2.2.62/vcredist_x86_VS2010.exe /q /norestart
wine64 /mprcsoft/MSFileReader-2.2.62/MSFileReader.exe /s /f1"c:\temp\msf_answers.iss" /f2"c:\temp\msf_log.log" /SMS
```

```bash
wine64 /mprcsoft/MSFileReader-2.2.62/MSFileReader.exe /uninst
```

```bash
wine64 /mprcsoft/MSFileReader-2.2.62/MSFileReader.exe /extract_all:"c:\temp\msf2"

wine64 /mprcsoft/MSFileReader-2.2.62/MSFileReader.exe /f2"c:\temp\msf_log.log"

wine64 /mprcsoft/reg/RegScanner.exe
mkdir -p /wineprefix64/drive_c/temp && wine64 /mprcsoft/msf/MSFileReader_3.1SP2_x64.exe /r /f1"c:\temp\setup.iss" /f2"c:\temp\setup_log.iss"
```

```bash
docker run -it -v ${HOME}/mprc:/data -v ${HOME}/mprcsoft:/mprcsoft -v ${HOME}/mprcsoft/drivec:/wineprefix64/drive_c -v /private/tmp:/private/tmp -e DISPLAY=host.docker.internal:0 rawdump wine64 /mprcsoft/rawExtract/0.6/MprcExtractRaw.exe --params /data/test_wine.params
```

