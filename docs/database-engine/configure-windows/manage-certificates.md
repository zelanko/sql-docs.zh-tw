---
title: 憑證管理 (SQL Server 組態管理員) | Microsoft Docs
description: 了解如何在各種 SQL Server 組態中安裝憑證。 範例包括單一執行個體、容錯移轉叢集和 Always On 可用性群組。
ms.custom: ''
ms.date: 01/16/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 835d0b1da11ba014b14ede9637117357e84dc208
ms.sourcegitcommit: d498110ec0c7c62782fb694d14436f06681f2c30
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/22/2020
ms.locfileid: "85196045"
---
# <a name="certificate-management-sql-server-configuration-manager"></a>憑證管理 (SQL Server 組態管理員)

本主題描述如何在您的 SQL Server Always On 容錯移轉叢集或可用性群組拓撲之間部署及管理憑證。

SSL/TLS 憑證普遍用來保護 SQL Server 的存取。 在舊版 SQL Server 中，具有大型 SQL Server 資產的組織必須花費相當多的心力來維護其 SQL Server 憑證基礎結構，通常是透過開發指令碼和執行手動命令。 在 SQL Server 2019 中，憑證管理已整合到 SQL Server 組態管理員中，並簡化一般工作，例如： 

* 檢視和驗證 SQL Server 執行個體中所安裝的憑證。 
* 識別哪些憑證可能即將到期。 
* 從保留主要複本的節點，在 Always On 可用性群組機器之間部署憑證。 
* 從作用中節點，在參與 Always On 容錯移轉叢集執行個體的機器之間部署憑證。

> [!NOTE]
> 您可以使用舊版 SQL Server (從 SQL Server 2008 開始) 隨附 SQL Server 組態管理員中的憑證管理。

##  <a name="to-install-a-certificate-for-a-single-sql-server-instance"></a><a name="provision-single-server-cert"></a> 安裝單一 SQL Server 執行個體的憑證  
  
1. 在 SQL Server 組態管理員的主控台窗格中，展開 [SQL Server 網路組態]。  
  
2. 以滑鼠右鍵按一下 [&lt;執行個體名稱&gt; 的通訊協定]，然後選取 [屬性]。  
  
3. 選擇 [憑證] 索引標籤，然後選取 [匯入]。  
  
4. 選取 [瀏覽]，然後選取憑證檔案。  
  
5. 選取 [下一步] 驗證憑證。 如果沒有任何錯誤，請選取 [下一步] 將憑證匯入本機執行個體。  
  
 
##  <a name="to-install-a-certificate-in-a-failover-cluster-instance-configuration"></a><a name="provision-failover-cluster-cert"></a> 在容錯移轉叢集執行個體組態中安裝憑證  
  
1. 在 SQL Server 組態管理員的主控台窗格中，展開 [SQL Server 網路組態]。
  
2. 以滑鼠右鍵按一下 [&lt;執行個體名稱&gt; 的通訊協定]，然後選擇 [屬性]。 

3. 選擇 [憑證] 索引標籤，然後選取 [匯入]。

4. 選取憑證類型，並選擇只要針對目前節點或要針對每個叢集節點匯入。

5. 若要針對單一節點安裝，請選擇 [瀏覽] 並選取憑證檔案。 然後跳到步驟 8。

6. 若要針對每個節點安裝憑證，請選取 [下一步] 列出可能的擁有者節點。 系統會預先選取目前容錯移轉叢集執行個體的可能擁有者。

7. 選擇 [下一步] 選取要匯入的憑證。

8. 請在系統提示時輸入密碼。 驗證後，尋找是否有任何警告或錯誤。

9. 選取 [下一步] 匯入選取的憑證。

> [!NOTE]
> 在 Always On 容錯移轉叢集執行個體的作用中節點上完成這些步驟。 使用者必須具有所有叢集節點的管理員權限。

##  <a name="to-install-a-certificate-in-an-always-on-availability-group-configuration"></a><a name="provision-availability-group-cert"></a> 在 Always On 可用性群組組態中安裝憑證  
  
1. 在 SQL Server 組態管理員的主控台窗格中，展開 [SQL Server 網路組態]。
  
2. 以滑鼠右鍵按一下 [&lt;執行個體名稱&gt; 的通訊協定]，然後選取 [屬性]。  
  
3. 選擇 [憑證] 索引標籤，然後選取 [匯入]。  
  
4. 選擇憑證類型，然後選取 [下一步] 從已知的可用性群組清單中進行選取。  

5. 選取 [下一步] 選擇每個複本節點的憑證。 憑證檔案名稱應該符合節點的 NetBIOS 名稱。

6. 選取 [下一步] 匯入每個節點上的憑證。


> [!NOTE]
> 從保留可用性群組主要複本的節點，完成這些步驟。 使用者必須具有所有叢集節點的管理員權限。

