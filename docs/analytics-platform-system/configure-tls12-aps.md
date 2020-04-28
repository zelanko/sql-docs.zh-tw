---
title: 正在設定 TLS 1。2
description: 在 AP 中設定 TLS 1.2 的建議
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 988cac765a596b541d128b0b6190f6f228d95ee7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401257"
---
# <a name="configure-tls-12-in-aps"></a>設定 AP 中的 TLS 1。2

若要保護僅限使用 TLS 1.2 的 AP，您必須在所有實體和虛擬主機上明確停用其他通訊協定。 停用通訊協定需要變更登錄設定。 登錄變更需要重新開機虛擬和實體主機。

> [!WARNING]
> 這個區段、方法或工作包含說明如何修改登錄的步驟。 不過，如果您不正確地修改登錄，可能會造成資料遺失，而且需要重新安裝作業系統，就會發生嚴重的問題。 我們強烈建議您先備份登錄，然後再進行修改。 如此一來，如果發生問題，您就可以還原登錄。 如需如何備份和還原登錄的詳細資訊，請按一下以下文章編號，以檢視 Microsoft 知識庫中的文章：<br>
[322756](https://support.microsoft.com/help/322756)如何備份和還原 Windows 中的登錄

**啟用**
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

此外，在您的用戶端電腦上設定下列金鑰：如已安裝 AP SSIS 目的地介面卡的工具。
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```



