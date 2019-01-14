---
title: 設定用於遠端資料表複本的 Parallel Data Warehouse |Microsoft Docs
description: 描述如何設定要使用之遠端資料表複製功能，將資料表複製到非應用裝置伺服器上 SMP SQL Server 資料庫的平行處理資料倉儲。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: fdac0b6ed211e223c3fad7ba15ac79a282c61303
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54123909"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>設定平行處理資料倉儲用於遠端資料表複本
描述如何設定要使用之遠端資料表複製功能，將資料表複製到非應用裝置伺服器上 SMP SQL Server 資料庫的 SQL Server PDW。  
  
本主題說明設定遠端資料表複製的組態步驟的其中一個。 如需所有設定步驟，請參閱[Remote Table copy 複製](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>開始之前  
若要設定使用遠端資料表複本的 SQL Server PDW 中，您必須：  
  
-   必須能夠直接將記錄的 Analytics Platform System 系統管理員帳戶 <strong>*appliance_domain*-AD01</strong>並 <strong>*appliance_domain*-Ad02 移</strong>節點。  
  
-   了解的主機名稱或 IP 目的地伺服器的名稱。  
  
## <a name="HowToPDW"></a>設定 SQL Server PDW 的遠端資料表複製：更新 DNS 中的主機名稱  
**CREATE REMOTE TABLE**陳述式，用於遠端資料表複本所使用的 IP 位址或 SMP Windows 系統的 IP 名稱指定目的地伺服器。 若要使用的 IP 名稱，您要新增至 DNS 伺服器的成功名稱解析的項目。  
  
下列步驟概述如何更新 DNS 伺服器。  
  
1.  登入作用中的 AD 節點 (通常 <strong>*appliance_domain*-AD01</strong>)。  
  
2.  開啟 [DNS 管理員]。 這位於**系統管理工具**中**開始**功能表。  
  
3.  使用 DNS 管理員新增的 IP 名稱。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[使用 DNS 轉寄站解析非設備 DNS 名稱](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
