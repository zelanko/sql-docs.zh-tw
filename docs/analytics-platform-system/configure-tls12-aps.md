---
title: 'Analytics Platform System 中設定 TLS 1.2 |Microsoft Docs '
description: 若要設定 TLS 1.2 中 AP 的建議
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5b6ea2144fe333f87123abdf92e16aa7122e98b4
ms.sourcegitcommit: 0f452eca5cf0be621ded80fb105ba7e8df7ac528
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2019
ms.locfileid: "57007551"
---
# <a name="configure-tls-12-in-aps"></a>在 AP 中設定 TLS 1.2

若要保護 AP，以只使用 TLS 1.2，您必須明確地停用所有實體和虛擬的主機上的其他通訊協定。 停用的通訊協定需要登錄設定變更。 登錄變更需要重新開機的虛擬和實體主機。

> [!WARNING]
> 這個區段、方法或工作包含說明如何修改登錄的步驟。 不過，如果您修改登錄不正確，可會造成資料遺失，而需要重新安裝作業系統的可能會發生嚴重的問題。 我們強烈建議您備份登錄再進行修改。 如此一來，如果發生問題，您就可以還原登錄。 如需有關如何備份和還原登錄，請按一下下列文章編號，以檢視 Microsoft 知識庫中的發行項的詳細資訊：<br>
[322756](https://support.microsoft.com/help/322756)如何備份及還原 Windows 中的登錄

**停用：**
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
```

也下列機碼上設定您的用戶端機器 AP SSIS 目的地配接器等工具的安裝位置。
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```



