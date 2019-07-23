---
title: 使用透明網路 IP 解析 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df5b0233168c52b4f79cdc6d2d03cd7b72e16046
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008483"
---
# <a name="using-transparent-network-ip-resolution"></a>使用透明網路 IP 解析
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution 是現有 MultiSubnetFailover 功能的修訂, 適用于 Microsoft ODBC Driver 13.1 for SQL Server, 其會影響驅動程式的連線順序 (如果主機名稱的第一個已解析 IP 不是)回應, 而且有多個與主機名稱相關聯的 Ip。 它會與 MultiSubnetFailover 互動, 以提供下列三個連接順序:

* 0: 嘗試一個 IP, 接著以平行方式執行所有 ip
* 1: 所有 Ip 都是以平行方式嘗試
* 2: 嘗試在另一個 Ip 之後逐一執行

|TransparentNetworkIPResolution|MultiSubnetFailover|行為|
|:-:|:-:|:-:|
|(預設值)|(預設值)|0|
|(預設值)|已啟用|1|
|(預設值)|已停用|0|
|已啟用|(預設值)|0|
|已啟用|已啟用|1|
|已啟用|已停用|0|
|已停用|(預設值)|2|
|已停用|已啟用|1|
|已停用|已停用|2|

`TransparentNetworkIPResolution`連接字串和 DSN 關鍵字會在連接字串層級控制此設定。 預設值為 [已啟用]。

關鍵字|值|預設
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

[ `SQL_COPT_SS_TNIR`預先連接] 屬性可讓應用程式以程式設計方式控制此設定:

連線屬性|   大小/類型|  預設| ReplTest1| Description
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` 或 `SQL_IS_UINTEGER`| `SQL_IS_ON`(1)、`SQL_IS_OFF`(0)|`SQL_IS_ON`|啟用或停用 TNIR。

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>如需 MultiSubnetFailover 的詳細資訊, 請參閱[Linux 和 macOS 上的 ODBC 驅動程式-高可用性和嚴重損壞修復](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>另請參閱  
* [Windows 上的 Microsoft ODBC Driver for SQL Server](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server 多重子網路叢集 (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
