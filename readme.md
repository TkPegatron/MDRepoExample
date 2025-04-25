<!-- Disable MDL subset for multiple top level header -->
<!-- markdownlint-disable MD025 -->
# Mitigation: Disable Deprecated TLS Versions

## Misc


```powershell
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -Force
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' –PropertyType 'DWORD' -Name 'Enabled' -Value '0' 
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' –PropertyType 'DWORD' -Name 'DisabledByDefault' -Value '1' 

New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -Force
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -PropertyType 'DWORD' -Name 'Enabled' -Value '0'
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' –PropertyType 'DWORD' -Name 'DisabledByDefault' -Value '1' 


New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -Force
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' –PropertyType 'DWORD' -Name 'Enabled' -Value '0' 
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' –PropertyType 'DWORD' -Name 'DisabledByDefault' -Value '1' 

New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -Force
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -PropertyType 'DWORD' -Name 'Enabled' -Value '0'
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' –PropertyType 'DWORD' -Name 'DisabledByDefault' -Value '1'
```

```powershell
New-ItemProperty -path "HKLM:\SOFTWARE\Microsoft\.NETFramework\v2.0.50727" -name 'SystemDefaultTlsVersions' -value 1 -PropertyType 'DWord' -Force | Out-Null
New-ItemProperty -path "HKLM:\SOFTWARE\Microsoft\.NETFramework\v2.0.50727" -name 'SchUseStrongCrypto' -value 1 -PropertyType 'DWord' -Force | Out-Null
New-ItemProperty -path "HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319" -name 'SystemDefaultTlsVersions' -value 1 -PropertyType 'DWord' -Force | Out-Null
New-ItemProperty -path "HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319" -name 'SchUseStrongCrypto' -value 1 -PropertyType 'DWord' -Force | Out-Null
if (Test-Path 'HKLM:\SOFTWARE\Wow6432Node') {
  New-ItemProperty -path "HKLM:\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727" -name 'SystemDefaultTlsVersions' -value 1 -PropertyType 'DWord' -Force | Out-Null
  New-ItemProperty -path "HKLM:\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727" -name 'SchUseStrongCrypto' -value 1 -PropertyType 'DWord' -Force | Out-Null
  New-ItemProperty -path "HKLM:\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319" -name 'SystemDefaultTlsVersions' -value 1 -PropertyType 'DWord' -Force | Out-Null
  New-ItemProperty -path "HKLM:\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319" -name 'SchUseStrongCrypto' -value 1 -PropertyType 'DWord' -Force | Out-Null
}
```

# Draft Documentation

sdjedf dhfsoifdhmsdaofs vfdvojfnsa
dfjhsdfg fgjosdfgngsfnh fdgsndgf hbonsggbnofgnbon 
fsgdbh osdg g nbdojgfbjnss dgobhnssdogfjbos fghfgqorhb  gsdfohg
fas hfogwns gff gbjsdghn ;gnbwjlnglsdfngs  fghsghnsdglfjnb

>[!WARNING]
> voksdhfg igjfjsfgroh hjggfhjsghojsdgjspdg ghjofgh
> 
> sdjfsouidfhbs fjgisdf f;dshj'idoghj gsdjgh:
> > sdfngkjshdfbsjdbhsdbsdfbd.fvsdfbhsdiofb.. fghsjofgahfvsefgv/fgosdfhgsf gshfogsfga

