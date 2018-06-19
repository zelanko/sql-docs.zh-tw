---
title: 連線到 dBASE 或其他 DBF 檔案 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to DBF files
- dBase files
- DBF files
ms.assetid: b0e8c831-9f96-475c-82a4-4f5b02692752
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5f69d97d9772fbb969da1fc6ccb52840fba98c9b
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35334612"
---
# <a name="connect-to-a-dbase-or-other-dbf-file"></a>連接到 dBASE 或其他 DBF 檔案
  您可以經由使用 OLE DB 連接管理員，並選取 Microsoft OLE DB Provider for Jet 4.0，連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中的 dBASE 或其他 .DBF 資料庫檔案。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的「SQL Server 匯入和匯出精靈」並不支援匯入或匯出 dBASE 或其他 DBF 檔案， 您可以使用 Microsoft Access 或 Microsoft Excel 將 DBF 檔案中的資料匯入 Access 資料庫或 Excel 試算表，然後再使用「SQL Server 匯入和匯出精靈」。  
  
### <a name="to-configure-a-connection-manager-to-connect-to-a-dbase-or-other-dbf-file"></a>設定連接管理員連接到 dBASE 或其他 DBF 檔案  
  
1.  將新的 OLE DB 連接管理員加入至封裝。 如需詳細資訊，請參閱[加入、刪除或共用封裝中的連線管理員](http://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)。  
  
2.  在 [連線管理員] 對話方塊的 [連接] 頁面上，選取 [原生 OLE DB\Microsoft Jet 4.0 OLE DB Provider] 作為 [提供者]。  
  
3.  使用 DBF 檔案時，資料夾代表資料庫，而個別 DBF 檔案則代表資料表。 因此，[資料庫檔名] 文字方塊必須包含 DBF 檔案所在的資料夾路徑，並且不可以包含檔案名稱本身。 您可以輸入或貼上資料夾路徑；或者是使用 [瀏覽] 按鈕選取 DBF 檔案，然後再移除資料夾路徑尾端的檔案名稱。  
  
4.  在 [連線管理員] 對話方塊的 [全部] 頁面上，依情況輸入 **dBASE III****dBASE IV** 或 **dBASE 5.0** 作為 [擴充屬性] 的值。  
  
5.  按一下 [測試連接] 驗證您輸入的值。 您應該會看到「連接測試成功」的訊息。 按一下 [確定] 關閉訊息方塊。  
  
6.  按一下 [確定] 儲存連線管理員的組態。  
  
7.  若要在封裝的資料流程中使用您的連接管理員，請選取 OLE DB 來源或目的地，並將它設定為使用您在先前步驟中所建立的連接管理員。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 連線管理員](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
  
