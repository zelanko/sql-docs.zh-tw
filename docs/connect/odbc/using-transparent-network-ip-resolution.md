---
title: 使用透明網路 IP 解析 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68070543e8fee326f0b5a02c73f0c0e4aaef6fbe
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928288"
---
# <a name="using-transparent-network-ip-resolution"></a>使用透明網路 IP 解析
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution 是 Microsoft ODBC Driver 13.1 for SQL Server 中現有 MultiSubnetFailover 功能的修訂，這會影響當主機名稱的第一個已解析 IP 無回應且有多個 IP 與該主機名稱相關聯時，驅動程式的連線順序。 這會與 MultiSubnetFailover 互動，以提供下列三個連線順序：

* 0：嘗試一個 IP，然後以並行方式嘗試所有 IP
* 1：以並行方式嘗試所有 IP
* 2：逐一嘗試所有 IP

|TransparentNetworkIPResolution|MultiSubnetFailover|Behaviour|
|:-:|:-:|:-:|
|(預設值)|(預設值)|0|
|(預設值)|啟用|1|
|(預設值)|已停用|0|
|啟用|(預設值)|0|
|啟用|啟用|1|
|啟用|已停用|0|
|已停用|(預設值)|2|
|已停用|啟用|1|
|已停用|已停用|2|

`TransparentNetworkIPResolution` 連接字串與 DSN 關鍵字會在連接字串等級控制此設定。 預設值為 [已啟用]。

關鍵字|值|預設
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

`SQL_COPT_SS_TNIR` 預先連接屬性可讓應用程式以程式設計方式控制此設定：

連線屬性|   大小/類型|  預設| 值| 描述
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` 或 `SQL_IS_UINTEGER`| `SQL_IS_ON`(1)、`SQL_IS_OFF`(0)|`SQL_IS_ON`|啟用或停用 TNIR。

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recovery"></a>如需 MultiSubnetFailover 的詳細資訊，請參閱 [Linux 和 macOS 上的 ODBC 驅動程式 - 高可用性和災害復原](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>另請參閱  
* [Windows 上的 Microsoft ODBC Driver for SQL Server](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server 多重子網路叢集 (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
