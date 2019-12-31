---
title: 遠端資料表複本
description: 描述如何設定平行處理資料倉儲，以使用遠端資料表複製功能，將資料表複製到非應用裝置伺服器上的 SMP SQL Server 資料庫。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6c9a0a29b543eb287c7e233d6b1ea77bb2a0d45c
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401258"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>設定遠端資料表複本的平行處理資料倉儲
描述如何設定 SQL Server PDW 使用遠端資料表複製功能，將資料表複製到非設備伺服器上的 SMP SQL Server 資料庫。  
  
本主題說明設定遠端資料表複本的其中一個設定步驟。 如需所有設定步驟的清單，請參閱[遠端資料表複本](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>開始之前  
若要將 SQL Server PDW 設定為使用遠端資料表複製，您必須：  
  
-   讓分析平臺系統管理員帳戶能夠直接登入<strong> *appliance_domain*-AD01</strong>和<strong> *appliance_domain*的 AD02</strong>節點。  
  
-   知道目的地伺服器的主機名稱或 IP 名稱。  
  
## <a name="HowToPDW"></a>設定遠端資料表複本的 SQL Server PDW：更新 DNS 中的主機名稱  
**CREATE REMOTE table**語句是用於遠端資料表複本，它會使用 SMP Windows 系統的 ip 位址或 ip 名稱來指定目的地伺服器。 若要使用 IP 名稱，您必須將成功名稱解析的專案新增至 DNS 伺服器。  
  
下列步驟概述如何更新 DNS 伺服器。  
  
1.  登入 active AD 節點（通常是<strong> *appliance_domain*-AD01</strong>）。  
  
2.  開啟 [DNS 管理員]。 這位於 [**開始**] 功能表中的 [系統**管理工具**] 底下。  
  
3.  使用 DNS 管理員來新增 IP 名稱。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[使用 DNS 轉寄站來解析非設備 DNS 名稱](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
