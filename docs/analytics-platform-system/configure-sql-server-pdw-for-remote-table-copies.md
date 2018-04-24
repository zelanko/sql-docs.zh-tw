---
title: 遠端資料表複本所需設定平行處理資料倉儲 |Microsoft 文件
description: 描述如何設定用於遠端資料表複製功能，將資料表複製到非應用裝置的伺服器上的 SMP SQL Server 資料庫的平行資料倉儲。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3f71a0c67639918820bca8f6f8f38b9f354154f3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>遠端資料表複本所需設定平行處理資料倉儲
描述如何設定用於遠端資料表複製功能，將資料表複製到非應用裝置的伺服器上的 SMP SQL Server 資料庫的 SQL Server PDW。  
  
本主題說明設定遠端資料表複製的組態步驟的其中一個。 如需所有設定步驟，請參閱[遠端資料表複製](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>開始之前  
若要設定 SQL Server PDW 使用遠端資料表的複本，您必須：  
  
-   有 Analytics Platform System 系統管理員帳戶，能夠登入直接 ***appliance_domain *-AD01**和 ***appliance_domain *-ad02 移**節點。  
  
-   了解的主機名稱或目的地伺服器的 IP 名稱。  
  
## <a name="HowToPDW"></a>設定為遠端資料表副本的 SQL Server PDW： 更新 DNS 中的主機名稱  
**CREATE REMOTE TABLE**陳述式，用於遠端資料表複本所使用的 IP 位址或 SMP Windows 系統的 IP 名稱指定目的地伺服器。 若要使用的 IP 名稱，您要新增至 DNS 伺服器的成功名稱解析項目。  
  
下列步驟概述如何更新 DNS 伺服器。  
  
1.  登入作用中的 AD 節點 (通常 ***appliance_domain *-AD01**)。  
  
2.  開啟 [DNS 管理員]。 這位於**系統管理工具**中**啟動**功能表。  
  
3.  使用 [DNS 管理員] 新增的 IP 名稱。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[使用 DNS 轉寄站 dns 名稱解析非應用裝置](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
