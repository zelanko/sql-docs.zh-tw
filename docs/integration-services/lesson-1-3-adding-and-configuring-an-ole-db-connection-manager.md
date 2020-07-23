---
title: 步驟 3：新增及設定 OLE DB 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 65ddfa851cce882d4106408ea99700d2cc57457c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917407"
---
# <a name="lesson-1-3-add-and-configure-an-ole-db-connection-manager"></a>課程 1-3：新增及設定 OLE DB 連線管理員

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



在新增「一般檔案」連線管理員來連線到資料來源之後，您需新增 OLE DB 連線管理員來連線到目的地。 OLE DB 連接管理員可讓封裝從任何 OLE DB 相容資料來源擷取資料或載入資料至該處。 使用 OLE DB 連線管理員時，您可以為連線指定伺服器、驗證方法及預設的資料庫。  
  
在本課程中，您會建立使用「Windows 驗證」來連線到 **AdventureWorksDW2012** 本機執行個體的 OLE DB 連線管理員。 您在本教學課程中稍後建立的其他元件 (例如「查閱」轉換和 OLE DB 目的地) 也會參考此 OLE DB 連線管理員。  
  
## <a name="add-and-configure-an-ole-db-connection-manager"></a>新增及設定 OLE DB 連線管理員

1. 在 [方案總管]  窗格中，於 [連線管理員]  上按一下滑鼠右鍵，然後選取 [新增連線管理員]  。

1. 在 [加入 SSIS 連線管理員]  對話方塊中，依序選取 [OLEDB]  和 [加入]  。
    
2. 在 [設定 OLE DB 連線管理員]  對話方塊中，選取 [新增]  。  
  
3. 對於 **[伺服器名稱]** ，輸入 **localhost**。  
  
    當您指定 localhost 做為伺服器名稱時，連接管理員會連接到本機電腦上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的預設執行個體。 若要使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的遠端執行個體，請將 localhost 取代成您要連接的伺服器名稱。  
  
4. 在 **[登入伺服器]** 群組中，確認已選取 **[使用 Windows 驗證]** 。  
  
5. 在 **[連接到資料庫]** 群組的 **[選取或輸入資料庫名稱]** 方塊中，輸入或選取 **AdventureWorksDW2012**。  
  
6. 選取 [測試連線]  以確認您指定的連線設定有效。  
  
7. 選取 [確定]  。  
  
8. 選取 [確定]  。  
  
9. 在 [連線管理員]  窗格中，確認已選取 [localhost.AdventureWorksDW2012]  。  
  

## <a name="go-to-next-task"></a>移至下一個工作
[步驟 4：將資料流程工作新增至套件](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>另請參閱  
[[無快取]](../integration-services/connection-manager/ole-db-connection-manager.md)  
  
