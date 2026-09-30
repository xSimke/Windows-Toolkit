@echo off
mode con: cols=62 lines=20
title Windows Toolkit
color 0b

:: PROVERA ADMINISTRATORSKIH PRAVA
net session >nul 2>&1
if %errorLevel% neq 0 (
    cls
    echo =============================================================
    echo                       ERROR: ACCESS DENIED                    
    echo =============================================================
    echo.
    echo  [!] You are NOT running this program as an Administrator.
    echo.
    echo  To fix this:
    echo  1. Close this window.
    echo  2. Right-click on this .bat file.
    echo  3. Select "Run as administrator".
    echo.
    echo =============================================================
    pause
    exit
)

:meni
cls
echo =============================================================
echo                       WINDOWS TOOLKIT                         
echo =============================================================
echo.
echo   [1] Check Windows Activation Status
echo   [2] Flush DNS ^& Reset Network Adapters
echo   [3] Run System File Checker (SFC Scan)
echo   [4] Run DISM System Repair
echo   [5] Check Disk for Errors (Chkdsk)
echo   [6] Open Master Control Panel
echo   [7] Clear Windows Update Cache
echo   [8] Battery Report (laptops)
echo   [9] System Info
echo   [0] Exit
echo.
echo =============================================================
echo.

set /p izbor=Select an option [1-7] and press Enter: 

if "%izbor%"=="1" goto status
if "%izbor%"=="2" goto internet
if "%izbor%"=="3" goto sfc
if "%izbor%"=="4" goto dism
if "%izbor%"=="5" goto chkdsk
if "%izbor%"=="6" goto master_panel
if "%izbor%"=="7" goto update_cache
if "%izbor%"=="8" goto battery_report
if "%izbor%"=="9" goto sys_info
if "%izbor%"=="0" goto exit 
goto meni

:status
cls
echo =============================================================
echo                 WINDOWS ACTIVATION STATUS
echo =============================================================
echo.
<nul set /p =[1/1] Fetching activation status
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
echo.
cscript //nologo %windir%\system32\slmgr.vbs /xpr
echo.
echo =============================================================
pause
goto meni

:internet
cls
echo =============================================================
echo                RESETTING NETWORK SETTINGS
echo =============================================================
echo.
<nul set /p =[1/4] Flushing DNS Cache
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
ipconfig /flushdns >nul
echo.
<nul set /p =[2/4] Resetting Winsock Catalog
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
netsh winsock reset >nul
echo.
<nul set /p =[3/4] Resetting TCP/IP Stack
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
netsh int ip reset >nul
echo.
<nul set /p =[4/4] Releasing ^& Renewing IP Address
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
ipconfig /release >nul
ipconfig /renew >nul
echo.
echo =============================================================
echo [SUCCESS] Network adapters and IP stacks have been rebuilt.
echo (Note: A system restart is REQUIRED for full effect).
echo =============================================================
pause
goto meni


:sfc
cls
echo =============================================================
echo                RUNNING SYSTEM FILE CHECKER
echo =============================================================
echo.
<nul set /p =[1/1] Initializing System File Checker
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
echo [INFO] This process may take a few minutes...
echo.
sfc /scannow
echo.
echo =============================================================
echo [PROCESS COMPLETED]
echo =============================================================
pause
goto meni

:chkdsk
cls
echo =============================================================
echo                     RUNNING CHECK DISK
echo =============================================================
echo.
<nul set /p =[1/1] Preparing disk scan
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
echo [INFO] Scanning the main drive for file system errors...
echo.
chkdsk c:
echo.
echo =============================================================
echo [PROCESS COMPLETED]
echo =============================================================
pause
goto meni

:master_panel
cls
echo =============================================================
echo               OPENING MASTER CONTROL PANEL
echo =============================================================
echo.
<nul set /p =[1/1] Launching advanced configuration console
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
start shell:::{ED7BA470-8E54-465E-825C-99712043E01C}
timeout /t 1 >nul
goto meni

:update_cache
cls
echo =============================================================
echo                CLEARING WINDOWS UPDATE CACHE
echo =============================================================
echo.
<nul set /p =[1/3] Stopping Windows Update services
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
net stop wuauserv >nul 2>&1
net stop bits >nul 2>&1
echo.
<nul set /p =[2/3] Deleting temporary update files
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
del /f /q /s "%windir%\SoftwareDistribution\Download\*.*" >nul 2>&1
echo.
<nul set /p =[3/3] Restarting Windows Update services
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
echo.
net start wuauserv >nul 2>&1
net start bits >nul 2>&1
echo.
echo =============================================================
echo [SUCCESS] Windows Update cache has been cleared.
echo =============================================================

:sys_info
cls
echo =============================================================
echo                SYSTEM HARDWARE SUMMARY
echo =============================================================
echo.
echo [PROCESSOR]:
powershell -Command "Get-CimInstance Win32_Processor | Select-Object -ExpandProperty Name"
echo.
echo [RAM]:
powershell -Command "$mem = (Get-CimInstance Win32_PhysicalMemory | Measure-Object -Property Capacity -Sum).Sum; [Math]::Round($mem / 1GB, 0).ToString() + ' GB RAM'"
echo.
echo [GRAPHICS]:
powershell -Command "Get-CimInstance Win32_VideoController | Select-Object -ExpandProperty Name"
echo.
echo [OS VERSION]:
powershell -Command "(Get-CimInstance Win32_OperatingSystem).Caption"
echo =============================================================
pause
goto meni
:battery_report
cls
echo =============================================================
echo                GENERATING BATTERY HEALTH REPORT
echo =============================================================
echo.
<nul set /p =        [1/2] Checking system type
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
<nul set /p =.
timeout /t 1 >nul
:: PowerShell proverava bateriju i upisuje rezultat u privremenu varijablu
for /f "delims=" %%i in ('powershell -Command "if (Get-CimInstance Win32_Battery) { echo Laptop } else { echo Desktop }"') do set "systemType=%%i"

if "%systemType%"=="Desktop" (
    echo.
    echo.
    echo =============================================================
    echo                   ERROR: NO BATTERY FOUND                    
    echo =============================================================
    echo.
    echo [!] This system appears to be a Desktop PC.
    echo [!] Battery reports are only available on laptops.
    echo.
    echo =============================================================
    pause
    goto meni
)

echo Done.
echo.
<nul set /p =        [2/2] Analysing battery logs . . .
timeout /t 1 >nul
powercfg /batteryreport /output "%temp%\battery_report.html" >nul
echo Done.
echo.
echo =============================================================
echo    [SUCCESS] Battery health report generated successfully!
echo    [INFO]    Opening the HTML report in your browser...
echo =============================================================
start "" "%temp%\battery_report.html"
pause
goto meni


echo.
<nul set /p =[2/2] Analysing battery logs
<nul set /p =.
timeout /t 1 >nul
echo.
powercfg /batteryreport /output "%temp%\battery_report.html" >nul
echo [SUCCESS] Report generated successfully.
echo.
echo [INFO] Opening the report in your browser...
start "" "%temp%\battery_report.html"
echo.
echo =============================================================
	
:dism
cls
echo =============================================================
echo                RUNNING DISM SYSTEM REPAIR
echo =============================================================
echo.
<nul set /p =[1/1] Checking and repairing component store
<nul set /p =.
timeout /t 1 >nul
echo.
echo [INFO] This process connects to Microsoft servers and may take a while...
echo.
dism /online /cleanup-image /restorehealth
echo.
echo =============================================================
echo [PROCESS COMPLETED]
echo =============================================================
pause
goto meni

:izlaz
exit
