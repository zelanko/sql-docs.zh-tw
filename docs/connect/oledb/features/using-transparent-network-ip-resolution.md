---
description: 使用透明網路 IP 解析
title: 使用透明網路 IP 解析 | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: chris-rossi
ms.author: v-chross
ms.openlocfilehash: adaad0f80d6304c855af22f134d24f0d3f23d301
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88415014"
---
# <a name="using-transparent-network-ip-resolution"></a>使用透明網路 IP 解析
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>目的
透明網路 IP 解析 (TNIR) 是現有 MultiSubnetFailover 功能的修訂版本。 如果第一個解析的主機名稱 IP 未回應，且該主機名稱有多個相關聯的 IP 時，TNIR 會影響驅動程式的連線順序。 TNIR 會與 MultiSubnetFailover 互動，以提供下列三種連線順序：<br />
* 0：嘗試一個 IP，然後以並行方式嘗試所有 IP
* 1：以並行方式嘗試所有 IP
* 2：逐一嘗試所有 IP

|TransparentNetworkIPResolution|MultiSubnetFailover|行為|
|--------|--------|--------|
|True|True|1|
|True|否|0|
|False|True|1|
|False|False|2|

## <a name="setting-transparent-network-ip-resolution"></a>設定透明網路 IP 解析
TransparentNetworkIPResolution 預設為啟用。 MultiSubnetFailover 預設為停用。 下列頁面提供有關設定這些屬性的詳細資訊： 
- [利用 OLE DB Driver for SQL Server 使用連接字串關鍵字](..\applications\using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [初始化和授權屬性](..\ole-db-data-source-objects\initialization-and-authorization-properties.md)

## <a name="see-also"></a>另請參閱 
[OLE DB Driver for SQL Server 支援高可用性、災害復原](./oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)
