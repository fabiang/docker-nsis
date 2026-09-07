# escape=`

ARG WINDOWS_IMAGE=servercore
ARG WINDOWS_VERSION=ltsc2022

FROM mcr.microsoft.com/windows/${WINDOWS_IMAGE}:${WINDOWS_VERSION}

SHELL ["C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe", "-NoLogo", "-NoProfile", "-Command"]

ARG NSIS_VERSION=3.12

ENV NSIS_HOME="C:\\Program Files (x86)\\NSIS"
ENV NSIS_VERSION="${NSIS_VERSION}"
ENV PATH="${NSIS_HOME};${PATH}"

RUN $ErrorActionPreference = 'Stop'; `
	$downloadUrl = ('https://' + 'master.dl.sourceforge.net/project/nsis/NSIS%203/' + $env:NSIS_VERSION + '/nsis-' + $env:NSIS_VERSION + '.zip'); `
	$archivePath = 'C:\nsis.zip'; `
	$webClient = New-Object System.Net.WebClient; `
	$webClient.DownloadFile($downloadUrl, $archivePath); `
	$webClient.Dispose(); `
	Expand-Archive -Path $archivePath -DestinationPath 'C:\'; `
	New-Item -ItemType Directory -Path $env:NSIS_HOME -Force | Out-Null; `
	Move-Item -Path "C:\nsis-$env:NSIS_VERSION\*" -Destination $env:NSIS_HOME; `
	Remove-Item "C:\nsis-$env:NSIS_VERSION" -Recurse; `
	Remove-Item $archivePath; `
	Get-Item "$env:NSIS_HOME\makensis.exe"

WORKDIR C:\installer
ENTRYPOINT ["makensis.exe"]
