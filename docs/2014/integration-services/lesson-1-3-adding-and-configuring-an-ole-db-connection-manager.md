---
title: 步驟 3：加入和設定 OLE DB 連線管理員 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c22c9ca183a5975b762fd166ee434f305422e6ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891717"
---
# <a name="step-3-adding-and-configuring-an-ole-db-connection-manager"></a>步驟 3：新增和設定 OLE DB 連線管理員
  在加入一般檔案連接管理員來連接到資料來源之後，下一項工作是加入 OLE DB 連接管理員來連接到目的地。 OLE DB 連接管理員可讓封裝從任何 OLE DB 相容資料來源擷取資料或載入資料至該處。 使用 OLE DB 連接管理員，您可以指定連接的伺服器、驗證方法和預設資料庫。  
  
 在這一課，您將建立 OLE DB 連接管理員，以便使用 Windows 驗證連接到 **AdventureWorksDB2012**的本機執行個體。 您建立的 OLE DB 連接管理員，也會供您在這個教學課程後面建立的其他元件所參考，例如查閱轉換和 OLE DB 目的地。  
  
### <a name="to-add-and-configure-an-ole-db-connection-manager-to-the-ssis-package"></a>若要將 OLE DB 連接管理員加入至 SSIS 封裝並進行設定  
  
1.  以滑鼠右鍵按一下 **[連接管理員]** 區域的任何位置，然後按一下 **[新增 OLE DB 連接]** 。  
  
2.  在 **[設定 OLE DB 連接管理員]** 對話方塊中，按一下 **[新增]** 。  
  
3.  對於 **[伺服器名稱]** ，輸入 **localhost**。  
  
     當您指定 localhost 做為伺服器名稱時，連接管理員會連接到本機電腦上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的預設執行個體。 若要使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的遠端執行個體，請將 localhost 取代成您要連接的伺服器名稱。  
  
4.  在 **[登入伺服器]** 群組中，確認已選取 **[使用 Windows 驗證]** 。  
  
5.  在 **連接到資料庫**群組中**選取或輸入資料庫名稱**方塊中，輸入或選取`AdventureWorksDW2012`。  
  
6.  按一下 **[測試連接]** 以確認您指定的連接設定有效。  
  
7.  按一下 [確定]  。  
  
8.  按一下 [確定]  。  
  
9. 在 **[設定 OLE DB 連接管理員]** 對話方塊的 **[資料連接]** 窗格中，確認已選取 **localhost.AdventureWorksDW2012** 。  
  
10. 按一下 [確定]  。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 4：將資料流程工作加入封裝](lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 連接管理員](connection-manager/ole-db-connection-manager.md)  
  
  
