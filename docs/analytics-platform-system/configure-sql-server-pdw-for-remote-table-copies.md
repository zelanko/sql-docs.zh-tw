---
title: "設定 SQL Server PDW 遠端資料表複製 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 496b4214-5891-404c-8237-c2a1e09db6d5
caps.latest.revision: "11"
ms.openlocfilehash: 08257e4823eed7bf86977ddca1df41eee7f8bda2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="configure-sql-server-pdw-for-remote-table-copies"></a>設定為遠端資料表複製的 SQL Server PDW
描述如何設定用於遠端資料表複製功能，將資料表複製到非應用裝置的伺服器上的 SMP SQL Server 資料庫的 SQL Server PDW。  
  
本主題說明設定遠端資料表複製的組態步驟的其中一個。 如需所有設定步驟，請參閱[遠端資料表複製](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>開始之前  
若要設定 SQL Server PDW 使用遠端資料表的複本，您必須：  
  
-   有 Analytics Platform System 系統管理員帳戶，能夠登入直接 ***appliance_domain*-AD01**和 ***appliance_domain*-Ad02 移**節點。  
  
-   了解的主機名稱或目的地伺服器的 IP 名稱。  
  
## <a name="HowToPDW"></a>設定為遠端資料表副本的 SQL Server PDW： 更新 DNS 中的主機名稱  
**CREATE REMOTE TABLE**陳述式，用於遠端資料表複本所使用的 IP 位址或 SMP Windows 系統的 IP 名稱指定目的地伺服器。 若要使用的 IP 名稱，您要新增至 DNS 伺服器的成功名稱解析項目。  
  
下列步驟概述如何更新 DNS 伺服器。  
  
1.  登入作用中的 AD 節點 (通常 ***appliance_domain*-AD01**)。  
  
2.  開啟 [DNS 管理員]。 這位於**系統管理工具**中**啟動**功能表。  
  
3.  使用 [DNS 管理員] 新增的 IP 名稱。  
  
## <a name="see-also"></a>請參閱  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[使用 DNS 轉寄站 dns 名稱解析非應用裝置](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
