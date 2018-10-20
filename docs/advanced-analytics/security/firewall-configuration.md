---
title: SQL Server Machine Learning 服務的防火牆設定 |Microsoft Docs
description: 如何設定 SQL Server Machine Learning 服務的防火牆。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: d2bf36ea9a7c7a0b193dc4613f6a36f58e66014a
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419053"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning 服務的防火牆設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文列出的系統管理員或架構設計人員應該謹記在心時使用 machine learning 服務的防火牆組態考量。

## <a name="default-firewall-rules"></a>預設的防火牆規則

根據預設，SQL Server 安裝程式會停用輸出連線，藉由建立防火牆規則。

在 SQL Server 2016 和 2017年中，這些規則根據本機使用者帳戶，安裝程式建立的一項輸出規則的所在**SQLRUserGroup** ，拒絕網路存取其成員 （每個背景工作帳戶已列為受到本機原則此規則。 如需 SQLRUserGroup 的詳細資訊，請參閱[SQL Server Machine Learning 服務的擴充性架構的安全性概觀](../../advanced-analytics/concepts/security.md#sqlrusergroup)。

在 SQL Server 2019，改為 AppContainers，過程有 AppContainer Sid 為基礎的新防火牆規則： 一個用於每個 20 AppContainers 建立 SQL Server 安裝程式。 防火牆規則名稱的命名慣例**AppContainer 00 封鎖網路存取 SQL Server 執行個體 MSSQLSERVER 中**其中 00 AppContainer (00-20 預設)，數目，是 MSSQLSERVER 是 SQL 的名稱伺服器執行個體。

> [!Note]
> 如果需要網路呼叫，您可以停用 Windows 防火牆中的輸出規則。

## <a name="restrict-network-access"></a>限制網路存取

在預設安裝中，Windows 防火牆規則來封鎖來自外部的執行階段處理序的所有輸出網路存取。 應該建立防火牆規則，以防止外部的執行階段處理序，下載封裝或進行其他可能是惡意的網路呼叫。

如果您使用其他防火牆程式，您也可以建立規則來封鎖外部的執行階段的輸出網路連線，藉由設定規則的本機使用者帳戶或使用者帳戶集區所代表的群組。

我們強烈建議您開啟 Windows 防火牆 （或您選擇的其他防火牆） 來防止不受限制的網路存取的 R 或 Python 執行階段。

## <a name="next-steps"></a>後續步驟

[設定傳入連接的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)