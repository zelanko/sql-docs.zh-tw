---
title: 使用透明網路 IP 解析 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d76e50b4761e8d1a32bbcfc4606778f96513ed1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852226"
---
# <a name="using-transparent-network-ip-resolution"></a>使用透明網路 IP 解析
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

則 TransparentNetworkIPResolution 是現有 MultiSubnetFailover 中, 可用功能的 Microsoft ODBC Driver 13.1 for SQL Server 會影響連接順序，其中主機名稱的第一個解決的 IP 並不會的案例中的驅動程式的修訂回應，有多個主機名稱相關聯的 Ip。 它與 MultiSubnetFailover 提供下列三個連接順序互動：

* 0： 其中一個嘗試 IP，後面接著平行中的所有 Ip
* 1： 嘗試以平行方式進行的所有 Ip
* 2： 嘗試進行的所有 Ip，依序

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

`TransparentNetworkIPResolution`連接字串和 DSN 關鍵字會控制這項設定在連接字串的層級。 預設為啟用。

關鍵字|值|預設值
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

`SQL_COPT_SS_TNIR`預先連接屬性可讓應用程式來控制此以程式設計方式設定：

連接屬性|   大小/類型|  預設值| Value| Description
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER`或`SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|啟用或停用 TNIR。

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>如需 MultiSubnetFailover 的詳細資訊，請參閱[ODBC Driver on Linux 及 macOS-高可用性和災害復原](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>另請參閱  
* [Windows 上的 Microsoft ODBC Driver for SQL Server](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server 多重子網路叢集 (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
