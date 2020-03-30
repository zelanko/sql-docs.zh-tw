---
title: 檢視 Windows 應用程式記錄檔 (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- application logs [SQL Server]
- logs [SQL Server], application
- monitoring Windows NT application log [SQL Server]
- Windows NT application logs [SQL Server]
- displaying logs
- monitoring [SQL Server], events
- logs [SQL Server], viewing
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2d6045c17028c16dfb2b90de15042dd18e3a91a2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "67986622"
---
# <a name="view-the-windows-application-log-windows-10"></a>檢視 Windows 應用程式記錄檔 (Windows 10)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為使用 Windows 應用程式記錄檔時，每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作階段都會將新事件寫入該記錄檔。 您每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，並不會建立新的應用程式記錄檔，這和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]錯誤記錄檔不同。  
  
## <a name="view-the-windows-application-log"></a>檢視 Windows 應用程式記錄檔  
  
1. 在**搜尋列** 中鍵入**事件檢視器**，然後選取 [事件檢視器]  傳統型應用程式。
  
2. 在 [事件檢視器]  中，開啟 [應用程式及服務記錄檔]  。

3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件是以 [來源]  資料行的 **MSSQLSERVER** 項目識別 (具名執行個體則是以 _MSSQL$_ **<執行個體名稱>** 識別)。 SQL Server Agent 事件由 SQLSERVERAGENT 項目識別 (對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具名執行個體，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 事件是由 **SQLAgent$** \<*執行個體名稱*> 加以識別)。 Microsoft Search 服務事件則以 **Microsoft Search**項目識別。  
  
4. 若要檢視不同電腦的記錄檔，請以滑鼠右鍵按一下 [事件檢視器 (本機)]  。 選取 [連線至其他電腦]  ，然後填入欄位以完成 [選取電腦]  對話方塊。  
  
5. (選擇性)，若只要顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件，請在 [檢視]  功能表上，選取 [篩選]  。 在 [事件來源]  清單中，選取 **MSSQLSERVER**。 若只想檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 事件，請改在 **[事件來源]** 清單中選取 **[SQLSERVERAGENT]** 。  
  
6. 若要檢視事件的詳細資訊，請按兩下該事件。  
  
## <a name="see-also"></a>另請參閱  
 [檢視 SQL Server 錯誤記錄檔 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  
