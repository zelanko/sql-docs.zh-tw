---
title: 防火牆組態
description: 如何設定防火牆以從 SQL Server Machine Learning 服務傳出連接。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c55f68a1134fee6477c52182ad66b8705e363296
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715590"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning 服務的防火牆設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文列出在使用機器學習服務時, 系統管理員或架構設計人員應該謹記的防火牆設定考慮。

## <a name="default-firewall-rules"></a>預設防火牆規則

根據預設, SQL Server 安裝程式會藉由建立防火牆規則來停用輸出連線。

在 SQL Server 2016 和2017中, 這些規則是以本機使用者帳戶為基礎, 其中安裝程式會為**SQLRUserGroup**拒絕對其成員進行網路存取的一條輸出規則 (每個背景工作帳戶均列為規則的本機原則)。 如需有關 SQLRUserGroup 的詳細資訊, 請參閱[SQL Server Machine Learning Services 中擴充性架構的安全性總覽](../../advanced-analytics/concepts/security.md#sqlrusergroup)。

在 SQL Server 2019 中, 在移至 AppContainers 的過程中, 會有以 AppContainer Sid 為基礎的新防火牆規則: 每個 SQL Server 安裝程式所建立的20個 AppContainers 都有一個。 防火牆規則名稱的命名慣例是**SQL Server 實例 MSSQLSERVER 中的 appcontainer-00 封鎖網路存取**, 其中00是 appcontainer 的數目 (預設為 00-20), 而 MSSQLSERVER 是 SQL Server 實例的名稱。

> [!Note]
> 如果需要網路呼叫, 您可以停用 Windows 防火牆中的輸出規則。

## <a name="restrict-network-access"></a>限制網路存取

在預設安裝中, 會使用 Windows 防火牆規則來封鎖外部執行時間進程的所有輸出網路存取。 應建立防火牆規則, 以防止外部執行時間進程下載封裝或進行其他可能為惡意的網路呼叫。

如果您使用不同的防火牆程式, 您也可以建立規則來封鎖外部執行時間的輸出網路連線, 方法是設定本機使用者帳戶或使用者帳戶集區所代表群組的規則。

強烈建議您開啟 Windows 防火牆 (或您選擇的另一個防火牆), 以防止 R 或 Python 執行時間進行不受限制的網路存取。

## <a name="next-steps"></a>後續步驟

[設定用於內建連接的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)