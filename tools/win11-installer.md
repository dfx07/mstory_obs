___
The Batch file to install necessary application.

```
@echo off

:: NOTE - Run as administrator

:: ///////////////////////////////////////////////////////
:: === Install Google Chrome ===

echo [*] Downloading Google Chrome...
powershell -Command "Invoke-WebRequest -Uri https://dl.google.com/chrome/install/latest/chrome_installer.exe -OutFile chrome_installer.exe"
echo [*] Installing Chrome...
start /wait chrome_installer.exe /silent /install
del chrome_installer.exe
color 0A
echo [=] Google Chrome installed complete!
color 07

:: ///////////////////////////////////////////////////////
:: === Install 7-Zip ===

echo [*] Downloading 7-Zip - 2501(x64)
powershell -Command "Invoke-WebRequest -Uri https://www.7-zip.org/a/7z2501-x64.exe -OutFile 7zip.exe"
echo [*] Installing 7-Zip...
start /wait 7zip.exe /S
del 7zip.exe
color 0A
echo [=] 7-Zip installed complete!
color 07

:: ///////////////////////////////////////////////////////
:: === Install Studio Code ===

echo [*] Downloading VS Code...
powershell -Command "Invoke-WebRequest -Uri https://update.code.visualstudio.com/latest/win32-x64-user/stable -OutFile vscode.exe"
echo [*] Installing VS Code...
start /wait vscode.exe /silent
del vscode.exe
color 0A
echo [=] VS Code installed complete! 
color 07

:: ///////////////////////////////////////////////////////
:: === Install UniKey Portable ===

echo [*] Downloading UniKey - 46RC2-230919(x64)
powershell -Command "Invoke-WebRequest -Uri https://www.unikey.org/assets/release/unikey46RC2-230919-win64.zip -OutFile unikey.zip"

echo [*] Unziping UniKey...
powershell -Command "Expand-Archive -Path unikey.zip -DestinationPath \"%ProgramFiles%\UniKey\" -Force"

echo [*] Create shortcut desktop...
powershell -Command "$s=(New-Object -COM WScript.Shell).CreateShortcut([Environment]::GetFolderPath('Desktop') + '\UniKey.lnk'); $s.TargetPath='%ProgramFiles%\UniKey\UniKeyNT.exe'; $s.Save()"

del unikey.zip
color 0A
echo [=] UniKey installed complete! 
color 07

:: ///////////////////////////////////////////////////////
:: === Install Notepad++ ===

echo [*] Downloading Notepad++ ...
powershell -Command "Invoke-WebRequest -Uri https://github.com/notepad-plus-plus/notepad-plus-plus/releases/download/v8.8.7/npp.8.8.7.Installer.x64.exe -OutFile npp_installer.exe"

echo [*] Installing Notepad++...
start /wait npp_installer.exe /S

del npp_installer.exe

color 0A
echo [=] Notepad++ installed complete! 
color 07

:: ///////////////////////////////////////////////////////
:: === Install Git ===

echo [*] Get last link Git...
for /f "delims=" %%i in ('powershell -NoProfile -Command "$url=(Invoke-RestMethod 'https://api.github.com/repos/git-for-windows/git/releases/latest').assets | Where-Object { $_.name -like '*64-bit.exe' } | Select-Object -First 1 -ExpandProperty browser_download_url; Write-Output $url"') do set "GIT_URL=%%i"

echo [*] Downloading Git...
powershell -Command "Invoke-WebRequest -Uri %GIT_URL% -OutFile git_installer.exe"

echo [*] Installing Git...
start /wait git_installer.exe /VERYSILENT /NORESTART

echo [*] Add to system path
set "gitPath=C:\Program Files\Git\cmd"
powershell -Command "[Environment]::SetEnvironmentVariable('Path', [Environment]::GetEnvironmentVariable('Path','User') + ';%gitPath%', 'User')"

:: Xoa file cai dat
del git_installer.exe

color 0A
echo [=] Git installed complete! 
color 07

:: ///////////////////////////////////////////////////////
:: === Install TortoiseGit ===

echo [*] Donwloading TortoiseGit - 2.17.0.2(x64)
powershell -Command "Invoke-WebRequest -Uri https://download.tortoisegit.org/tgit/2.17.0.0/TortoiseGit-2.17.0.2-64bit.msi -OutFile TortoiseGit_installer.msi"

echo [*] Installing (silent) ...
msiexec /i TortoiseGit_installer.msi

del TortoiseGit_installer.msi

color 0A
echo [=] TortoiseGit installed complete! 
color 07

:: ///////////////////////////////////////////////////////
:: === Install Obsidian ===

echo [*] Donwloading Obsidian - 1.9.14(x64)
powershell -Command "Invoke-WebRequest -Uri https://github.com/obsidianmd/obsidian-releases/releases/download/v1.9.14/Obsidian-1.9.14.exe -OutFile Obsidian_installer.exe"

echo [*] Installing (silent) ...
start /wait Obsidian_installer.exe /VERYSILENT /NORESTART

del Obsidian_installer.exe

color 0A
echo [=] Obsidian installed complete! 
color 07

:: ///////////////////////////////////////////////////////
:: === Install Teamviewer ===

echo [*] Donwloading Teamviewer newest(x64)
powershell -Command "Invoke-WebRequest -Uri https://download.teamviewer.com/download/TeamViewer_Setup_x64.exe -OutFile TeamViewer_installer.exe"

echo [*] Installing (silent) ...
start /wait TeamViewer_installer.exe /VERYSILENT /NORESTART

del Teamviewer_installer.exe

color 0A
echo [=] Teamviewer installed complete! 
color 07

:: ///////////////////////////////////////////////////////
:: === Install Lightshot ===

echo [*] Donwloading Lightshot (x64)
powershell -Command "Invoke-WebRequest -Uri https://app.prntscr.com/build/setup-lightshot.exe -OutFile lightshot_installer.exe"

echo [*] Installing (silent) ...
start /wait lightshot_installer.exe /VERYSILENT /NORESTART

del lightshot_installer.exe

color 0A
echo [=] Lightshot installed complete! 
color 07

:: ///////////////////////////////////////////////////////
:: === Install PowerToys (Version : 0.95.1)===

echo [*] Donwloading PowerToys - 0.95.1(x64)
powershell -Command "Invoke-WebRequest -Uri https://github.com/microsoft/PowerToys/releases/download/v0.95.1/PowerToysSetup-0.95.1-arm64.exe -OutFile PowerToys_installer.exe"

echo [*] Installing (silent) ...
start /wait PowerToys_installer.exe /VERYSILENT /NORESTART

del PowerToys_installer.exe

color 0A
echo [=] PowerToys installed complete! 
color 07


pause


```