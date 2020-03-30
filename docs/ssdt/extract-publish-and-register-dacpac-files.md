---
title: 擷取、發行及註冊 .dacpac 檔案
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.DacTableChooser
- sql.data.tools.DacPublishDialog
- sql.data.tools.DacPropertiesDialog
- sql.data.tools.publishdacproject
- sql.data.tools.DacExtractDialog
ms.assetid: ed900f93-d3df-40f5-8e62-4d722595e041
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 67cb0321ebc1bdfa345b7bb6670ca31a4418d6e8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241654"
---
# <a name="extract-publish-and-register-dacpac-files"></a>擷取、發行及註冊 .dacpac 檔案

本主題描述在 SQL Server 物件總管中以滑鼠右鍵按一下連接的資料庫即可執行的四個程序：  
  
-   發行資料層應用程式  
  
-   擷取資料層應用程式  
  
-   註冊資料層應用程式  
  
-   取消註冊資料層應用程式  
  
## <a name="publish-data-tier-application"></a>發行資料層應用程式  
您可以將 .dacpac 發行至資料庫。 發行動作會累加更新資料庫結構描述，以符合來源 .dacpac 檔案的結構描述。 如果資料庫不存在伺服器上，發行作業會加以建立。  
  
也可以透過選取 [資料庫] 節點，使用此動作。  
  
選取 .dacpac 檔案。 在您指定 .dacpac 檔案之後，[DAC 屬性]  按鈕便會啟用。 [DAC 屬性]  對話方塊會顯示 .dacpac 檔案的資訊。  
  
指定資料庫伺服器的連接字串，然後指定資料庫名稱 (如果連接字串中沒有資料庫名稱)。  
  
[發行]  和 [產生指令碼]  按鈕現在已啟用。 如果您產生指令碼，它會在文件視窗中開啟，可視需要予以儲存。 如果您選擇直接發行至資料庫，可在 [資料工具作業]  視窗中檢視更新摘要和實際使用的指令碼。  
  
核取時，[註冊為資料層應用程式]  核取方塊會使產生的資料庫註冊為伺服器中繼資料中的資料層應用程式。 如果發行的目標資料庫已註冊，當資料庫結構描述不同於其目前註冊的 dacpac 時，發行會失敗。  
  
[進階發行設定]  對話方塊中有其他發行組態，按一下 [進階]  按鈕可存取這個對話方塊。  
  
## <a name="extract-data-tier-application"></a>擷取資料層應用程式  
您可以從資料庫擷取 .dacpac。 擷取會從即時 SQL Server 或 Azure SQL Database 建立資料庫快照集檔案 (.dacpac)，不僅包含資料庫結構描述，可能還包含使用者資料表中的資料。  
  
指定要建立的 .dacpac 檔案。 [DAC 屬性]  按鈕會顯示 [DAC 屬性]  對話方塊，讓您指定 .dacpac 檔案的屬性。  
  
視需要修改擷取程序的組態。 在 [擷取設定]  區段中，您可以選擇只擷取結構描述或擷取結構描述並包含資料表資料。 如果選擇擷取結構描述和資料，可以選取要擷取資料的資料表。  
  
## <a name="register-data-tier-application"></a>註冊資料層應用程式  
您可將資料庫註冊為執行個體中的資料層應用程式 (DAC)。 這會將資料庫結構描述的目前狀態表示儲存在系統中繼資料中。  
  
在 [註冊資料層應用程式]  對話方塊中，指定已註冊的 DAC 屬性。  
  
## <a name="unregister-data-tier-application"></a>取消註冊資料層應用程式  
取消註冊可讓您從執行個體移除已註冊之資料層應用程式的中繼資料。 取消註冊不會刪除已註冊的資料庫。  
  
## <a name="see-also"></a>另請參閱  
[連接的資料庫開發](../ssdt/connected-database-development.md)  
  
