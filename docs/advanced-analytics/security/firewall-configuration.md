---
title: 防火牆組態
description: 如何針對 SQL Server 機器學習服務的輸出連線設定防火牆。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c55f68a1134fee6477c52182ad66b8705e363296
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "68715590"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>SQL Server 機器學習服務的防火牆組態
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文列出系統管理員或結構設計師在使用機器學習服務時，應該謹記的防火牆組態考量。

## <a name="default-firewall-rules"></a>預設防火牆規則

根據預設，SQL Server 安裝程式會藉由建立防火牆規則來停用輸出連線。

在 SQL Server 2016 和 2017 中，這些規則是以本機使用者帳戶為基礎，其中安裝程式會針對 **SQLRUserGroup** 建立一個輸出規則，該規則拒絕對其成員的網路存取 (每個背景工作角色帳戶都被列為受該規則約束的本機原則)。 如需 SQLRUserGroup 的詳細資訊，請參閱 [SQL Server 機器學習服務中擴充性架構的安全性概觀](../../advanced-analytics/concepts/security.md#sqlrusergroup)。

在 SQL Server 2019 內移至 AppContainers 的過程中，有一些以 AppContainer SID 為基礎的新防火牆規則：SQL Server 安裝程式所建立的 20 個 AppContainer 各有一個。 防火牆規則名稱的命名慣例是**在 SQL Server 執行個體 MSSQLSERVER 中封鎖 AppContainer-00 的網路存取**，其中 00 是 AppContainer 的數目 (預設為 00-20)，而 MSSQLSERVER 是 SQL Server 執行個體的名稱。

> [!Note]
> 如果需要網路呼叫，您可以停用 Windows 防火牆中的輸出規則。

## <a name="restrict-network-access"></a>限制網路存取

在預設安裝中，使用了一項 Windows 防火牆規則來封鎖從外部執行階段處理序傳出的所有網路存取。 您應該建立防火牆規則，以防止外部執行階段處理序下載套件或進行其他可能是惡意的網路呼叫。

如果您使用其他防火牆程式，也可以建立規則來封鎖外部執行階段傳出的網路連線，方法是設定本機使用者帳戶或使用者帳戶集區所代表群組的規則。

我們強烈建議您開啟 Windows 防火牆 (或您選擇的其他防火牆)，以防止 R 或 Python 執行階段進行的不受限制的網路存取。

## <a name="next-steps"></a>後續步驟

[設定用於輸入連線的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)