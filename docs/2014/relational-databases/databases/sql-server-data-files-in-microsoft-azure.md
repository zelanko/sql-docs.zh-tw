---
title: 在 Windows Azure 中的 SQL Server 資料檔案 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 38ffd9c2-18a5-43d2-b674-e425addec4e4
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5399380cb663f816b961a44fb76d437c1c8fec21
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134424"
---
# <a name="sql-server-data-files-in-windows-azure"></a>Windows Azure 中的 SQL Server 資料檔案
  Windows Azure 中的 SQL Server 資料檔案可提供將 SQL Server 資料庫檔案儲存為 Windows Azure Blob 的原生支援。 它可讓您在內部部署執行的 SQL Server 或 Windows Azure 虛擬機器執行的 SQL Server 中建立資料庫，以將您的 Windows Azure Blob 儲存體資料儲存在專用儲存位置。 此增強功能特別簡化了使用卸離和附加作業，在電腦之間移動資料庫的工作。 此外，它可讓您還原至 Windows Azure 儲存體或從中還原，為您的資料庫備份檔案提供替代儲存位置。 因此，它會針對資料虛擬化、資料移動、安全性和可用性提供許多優點，進而實現許多混合式方案，而且成本低廉、維護簡單，即可達到高可用性和彈性調整的效果。  
  
 本主題介紹將 SQL Server 資料檔案儲存在 Windows Azure 儲存體服務中的核心概念與考量。  
  
 如需如何使用這項新功能的實際操作體驗，請參閱[教學課程： Windows Azure 儲存體服務中的 SQL Server 資料檔案](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)。  
  
 下圖展示這個增強功能如何讓您將 SQL Server 資料庫檔案儲存成 Windows Azure 儲存體中的 Windows Azure Blob，不論您的伺服器位於何處都沒問題。  
  
 ![SQL Server 與 Windows 整合 Azure 儲存體](../../database-engine/media/sql-server-dbfiles-stored-as-blobs.gif "SQL Server 與 Windows 整合 Azure 儲存體")  
  
## <a name="benefits-of-using-sql-server-data-files-in-windows-azure"></a>在 Windows Azure 中使用 SQL Server 資料檔案的優點  
  
-   **簡單快速移轉優點：** 這項功能會在內部部署的電腦之間以及內部部署與雲端環境之間一次移動一個資料庫，藉以簡化移轉程序，而且不需要變更任何應用程式。 因此，它支援累加式移轉，同時就地維護您現有的內部部署基礎結構。 此外，當應用程式需要在內部部署環境中的多個位置執行時，存取集中式資料儲存體可簡化應用程式邏輯。 在某些情況下，您可能需要快速地設定散佈於不同地理位置的電腦中心，以便蒐集許多不同來源的資料。 只要使用這項新的增強功能，您就可以將許多資料庫儲存成 Windows Azure Blob，然後執行 Transact-SQL 指令碼，在本機電腦或虛擬機器上建立資料庫，而不需要在不同的位置之間移動資料。  
  
-   **成本和無限制儲存體優點：** 這項功能可讓您在 Windows Azure 中設有無限制的異地儲存體，同時運用內部部署運算資源。 當您將 Windows Azure 當做儲存位置使用時，可以輕鬆地將重點放在應用程式邏輯上，而不會產生硬體管理的負擔。 如果您遺失了某個內部部署的計算節點，不需要移動任何資料，就可以設定新的節點。  
  
-   **高可用性和災害復原優點：** Windows Azure 功能中使用 SQL Server 資料檔案可簡化高可用性和災害復原解決方案。 例如，假設某個 Windows Azure 虛擬機器或 SQL Server 執行個體當機，您只要重新建立 Windows Azure Blob 的連結，就可以在新的電腦中重建資料庫。  
  
-   **安全性優點** ：這項新的增強功能可讓您分隔計算執行個體與儲存執行個體。 您可以擁有完整加密的資料庫，而且只針對計算執行個體進行解密，但不在儲存執行個體中進行解密。 換言之，使用這項新的增強功能時，您可以使用透明資料加密 (TDE) 憑證 (與資料實體分隔) 來加密公用雲端中的所有資料。 TDE 金鑰可以儲存在 master 資料庫中，而這個資料庫會儲存在實體安全的內部部署電腦本機並且進行本機備份。 您可以使用這些本機金鑰來加密位於 Windows Azure 儲存體中的資料。 如果您的雲端儲存體帳戶認證遭竊，您的資料仍然保持安全，因為 TDE 憑證永遠位於內部部署。  
  
## <a name="concepts-and-requirements"></a>概念和需求  
  
### <a name="windows-azure-storage-concepts"></a>Windows Azure 儲存體概念  
 使用 Windows Azure 功能中的 SQL Server 資料檔案時，您必須在 Windows Azure 中建立儲存體帳戶和容器。 然後，您必須建立 SQL Server 認證，其中包括容器原則的相關資訊以及存取容器所需的共用存取簽章。  
  
 在 Windows Azure 中，儲存體帳戶代表存取 Blob 之命名空間的最高層級。 儲存體帳戶可以包含不限制數目的容器，只要其總大小低於 500 TB 即可。 如需有關儲存體限制的最新資訊，請參閱 [Azure 訂閱與服務限制、配額及條件約束](http://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/)。 容器會提供一組 Blob 的群組。 所有 Blob 都必須位於容器中。 帳戶可以包含不限制數目的容器。 同樣地，容器也可以儲存不限制數目的 Blob。 Windows Azure 儲存體可以儲存的 Blob 類型有兩種：區塊和分頁 Blob。 這項新功能使用的是分頁 Blob (大小最高可達 1TB)，而且當檔案中的位元組範圍經常修改時，更有效率。 您可以使用以下 URL 格式存取 Blob： `http://storageaccount.blob.core.windows.net/<container>/<blob>`。  
  
### <a name="windows-azure-billing-considerations"></a>Windows Azure 計費考量  
 在決策和規劃程序中，估計使用 Windows Azure 服務的成本是很重要的事項。 將 SQL Server 資料檔案儲存在 Windows Azure 儲存體中時，需要支付與儲存體和交易相關聯的成本。 此外，實作 Windows Azure 儲存體功能中的 SQL Server 資料檔案時，還需要每隔 45 至 60 秒，隱含地更新 Blob 租用一次。 這也會產生每個資料庫檔案 (例如 .mdf 或 .ldf) 的交易成本。 根據我們的估計，按照目前的定價模式，兩個資料庫檔案 (.mdf 和 .ldf) 更新租用的成本大約是每月 2 美分。 我們建議您使用 [Azure Pricing](http://azure.microsoft.com/pricing/) 頁面上的資訊來協助估計與使用 Windows Azure 儲存體和 Windows Azure 虛擬機器的每月相關成本。  
  
### <a name="sql-server-concepts"></a>SQL 伺服器概念  
 使用這項新的增強功能時，您必須執行下列動作：  
  
-   您必須在容器上建立原則，同時產生共用存取簽章 (SAS) 金鑰。  
  
-   對於資料或記錄檔所使用的每一個容器，您都必須建立名稱符合容器路徑的 SQL Server 認證。  
  
-   您必須將 Windows Azure 儲存體容器的相關資訊、其相關聯的原則名稱以及 SAS 金鑰，儲存在 SQL Server 認證存放區中。  
  
 下列範例會假設已經建立 Windows Azure 儲存體容器，而且已經建立具有讀取、寫入和列出權限的原則。 在容器上建立原則會產生 SAS 金鑰，這個金鑰會以未加密狀態安全地保存在記憶體中，而且 SQL Server 需要此金鑰才能存取容器中的 Blob 檔案。 在下列程式碼片段中，使用與下列類似的項目取代 `'your SAS key'` ： `'sr=c&si=<MYPOLICYNAME>&sig=<THESHAREDACCESSSIGNATURE>'`。 如需詳細資訊，請參閱[建立和使用共用存取簽章](http://msdn.microsoft.com/library/azure/jj721951.aspx)  
  
```  
  
-- Create a credential  
CREATE CREDENTIAL [https://testdb.blob.core.windows.net/data]  
WITH IDENTITY='SHARED ACCESS SIGNATURE',  
SECRET = 'your SAS key'  
  
-- Create database with data and log files in Windows Azure container.  
CREATE DATABASE testdb   
ON  
( NAME = testdb_dat,  
    FILENAME = 'https://testdb.blob.core.windows.net/data/TestData.mdf' )  
 LOG ON  
( NAME = testdb_log,  
    FILENAME =  'https://testdb.blob.core.windows.net/data/TestLog.ldf')  
  
```  
  
 **重要注意事項** ：如果有任何作用中參考指向容器中的資料檔案，則嘗試刪除對應的 SQL Server 認證將會失敗。  
  
### <a name="security"></a>Security  
 以下是將 SQL Server 資料檔案儲存在 Windows Azure 儲存體中的安全性考量和需求。  
  
-   建立 Windows Azure Blob 儲存體服務的容器時，建議您將存取權設為 [私用]。 當您將存取設為私用時，只有 Windows Azure 帳戶擁有者才能讀取容器和 Blob 資料。  
  
-   在 Windows Azure 儲存體中儲存 SQL Server 資料庫檔案時，您必須使用共用存取簽章，這是針對容器、Blob、佇列和資料表授與有限存取權限的 URI。 您可以使用共用存取簽章，讓 SQL Server 存取儲存體帳戶中的資源，而不需要共用您的 Windows Azure 儲存體帳戶金鑰。  
  
-   此外，我們建議您繼續針對資料庫實作傳統的內部部署安全性作法。  
  
### <a name="installation-prerequisites"></a>安裝的必要條件  
 以下是將 SQL Server 資料檔案儲存在 Windows Azure 中的安裝必要條件。  
  
-   **SQL Server 內部部署：** SQL Server 2014 版本包含這項功能。 若要了解如何下載 SQL Server 2014，請參閱＜ [SQL Server 2014](http://www.microsoft.com/sqlserver/sql-server-2014.aspx)＞。  
  
-   Windows Azure 虛擬機器中執行的 SQL Server： 如果您要安裝 SQL Server 在 Windows Azure 虛擬機器，安裝 SQL Server 2014 或更新現有的執行個體。 同樣地，您也可以使用 SQL Server 2014 平台映像，在 Windows Azure 中建立新的虛擬機器。 若要了解如何下載 SQL Server 2014，請參閱＜ [SQL Server 2014](http://www.microsoft.com/sqlserver/sql-server-2014.aspx)＞。  
  
###  <a name="bkmk_Limitations"></a> 限制  
  
-   這項功能，目前版本中儲存`FileStream`不支援 Windows Azure 儲存體中的資料。 您可以將 `Filestream` 資料儲存在 Windows Azure 儲存體整合的本機資料庫中，但是無法使用 Windows Azure 儲存體，在電腦之間移動 Filestream 資料。 如`FileStream`資料，我們建議您繼續使用傳統的技術移動與 Filestream 相關聯，不同的電腦之間的檔案 （.mdf、.ldf）。  
  
-   目前，這項新的增強功能不支援多個 SQL Server 執行個體同時存取 Windows Azure 儲存體中的相同資料庫檔案。 如果 ServerA 在線上且具有作用中的資料庫檔案，而 ServerB 意外啟動，而且也有指向相同資料檔案的資料庫，則第二部伺服器將無法啟動資料庫，錯誤碼為 **5120 無法開啟實體檔案 "%.\*ls"。作業系統錯誤 %d: "%ls"**。  
  
-   透過使用 Windows Azure 功能中的 SQL Server 資料檔案，僅能將 .mdf、.ldf 和 .ndf 檔案儲存在 Windows Azure 儲存體中。  
  
-   使用 Windows Azure 功能中的 SQL Server 資料檔案時，您的儲存體帳戶不支援異地備援。 如果儲存體帳戶進行異地備援，然後進行異地容錯移轉，可能會發生資料庫損毀。  
  
-   每個 Blob 的大小最高可達 1 TB。 這會針對 Windows Azure 儲存體可儲存的個別資料庫資料和記錄檔建立上限。  
  
-   您無法使用 Windows Azure 儲存體功能中的 SQL Server 資料檔案，將記憶體中的 OLTP 資料儲存在 Windows Azure Blob 中。 這是因為記憶體中 OLTP 會相依於`FileStream`，在目前版本的功能中，儲存`FileStream`不支援 Windows Azure 儲存體中的資料。  
  
-   使用 Windows Azure 功能中的 SQL Server 資料檔案時，SQL Server 會使用 `master` 資料庫中設定的定序執行所有 URL 或檔案路徑比較。  
  
-   只要您不要將新的資料庫檔案加入至主要資料庫，就支援 `AlwaysOn Availability Groups`。 如果資料庫作業需要在主要資料庫中建立新的檔案，請先在次要節點中停用 AlwaysOn 可用性群組。 然後，在主要資料庫上執行資料庫作業，並且備份主要節點中的資料庫。 接著，將資料庫還原到次要節點，並且在次要節點中啟用 AlwaysOn 可用性群組。 請注意，使用 Windows Azure 功能中的 SQL Server 資料檔案時，不支援 AlwaysOn 容錯移轉叢集執行個體。  
  
-   一般作業期間，SQL Server 會使用暫時租用來保留 Blob 進行儲存，而且每隔 45 至 60 秒就會更新每個 Blob 租用。 如果伺服器當機，而且設定為使用相同 Blob 的另一個 SQL Server 執行個體啟動，新的執行個體最多會等候 60 秒，讓現有的 Blob 租用過期。 如果您想要將資料庫附加至另一個執行個體，而且您無法等候租用在 60 秒內過期，可以明確中斷 Blob 租用，避免附加作業發生任何失敗。  
  
## <a name="tools-and-programming-reference-support"></a>工具和程式設計參考支援  
 本節說明將 SQL Server 資料檔案儲存在 Windows Azure 儲存體中時，可以使用哪些工具和程式設計參考資料庫。  
  
### <a name="powershell-support"></a>PowerShell 支援  
 在 SQL Server 2014 中，您可以使用 PowerShell Cmdlet，藉由參考 Blob 儲存體 URL 路徑而非檔案路徑，將 SQL Server 資料檔案儲存在 Windows Azure Blob 儲存體服務中。 您可以使用下列 URL 格式來存取 Blob`: http://storageaccount.blob.core.windows.net/<container>/<blob>` 。  
  
### <a name="sql-server-object-and-performance-counters-support"></a>SQL Server 物件和效能計數器支援  
 從 SQL Server 2014 開始，已加入新的 SQL Server 物件，以用於 Windows Azure 儲存體功能中的 SQL Server 資料檔案。 這個新的 SQL Server 物件稱為 [SQL Server:HTTP_STORAGE_OBJECT](../performance-monitor/sql-server-http-storage-object.md)，而且系統監視器可以在使用 Windows Azure 儲存體執行 SQL Server 時，使用此物件來監視活動。  
  
### <a name="sql-server-management-studio-support"></a>SQL Server Management Studio 支援  
 SQL Server Management Studio 可讓您經由許多對話方塊視窗使用此功能。 例如，您可以在許多對話方塊視窗 (例如 [新增資料庫] `https://teststorageaccnt.blob.core.windows.net/testcontainer/` 、 **[附加資料庫]** 和 **[還原資料庫]**) 中，輸入儲存體容器的 URL 路徑 (例如 ) 做為 **[路徑]**。 如需詳細資訊，請參閱[教學課程： Windows Azure 儲存體服務中的 SQL Server 資料檔案](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)。  
  
### <a name="sql-server-management-objects-support"></a>SQL Server 管理物件支援  
 使用 Windows Azure 功能中的 SQL Server 資料檔案時，可支援所有 SQL Server 管理物件 (SMO)。 如果 SMO 物件需要檔案路徑，請使用 BLOB URL 格式而非本機檔案路徑，例如 `https://teststorageaccnt.blob.core.windows.net/testcontainer/`。 如需 SQL Server 管理物件 (SMO) 的詳細資訊，請參閱《SQL Server 線上叢書》中的 [SQL Server 管理物件 &#40;SMO&#41; 程式設計指南](../server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)。  
  
### <a name="transact-sql-support"></a>Transact-SQL 支援  
 這項新功能已經在 Transact-SQL 介面區中導入下列變更：  
  
-   **sys.master_files** 系統檢視中的新 **int**資料行： **credential_id** 。 **credential_id** 資料行是用來讓啟用 Azure 儲存體的資料檔案能夠交互參考 sys.credentials，以便取得針對它們建立的認證。 您可以使用此資料行進行疑難排解，例如某個資料庫檔案正在使用認證，導致無法刪除認證時。  
  
##  <a name="bkmk_Troubleshooting"></a> 在 Windows Azure 中的 SQL Server 資料檔案疑難排解  
 為了避免因為功能不支援或有限制而發生錯誤，請先檢閱＜ [Limitations](sql-server-data-files-in-microsoft-azure.md#bkmk_Limitations)＞。  
  
 使用 Windows Azure 儲存體功能中的 SQL Server 資料檔案時，可能會收到的錯誤清單如下。  
  
 **驗證錯誤**  
  
-   *無法卸除認證 '%.\*ls'，因為作用中的資料庫檔案正在使用它。*   
    解決方式：當您嘗試卸除的認證仍然由 Windows Azure 儲存體中的作用中資料庫檔案使用時，就可能會看見此錯誤。 若要卸除認證，您必須先刪除具有此資料庫檔案的相關聯 Blob。 若要刪除擁有使用中租用的 Blob，您必須先中斷租用。  
  
-   *尚未在容器上正確建立共用存取簽章。*   
     解決方式：請確定您已經在容器上正確建立共用存取簽章。 檢閱中第 2 課所提供的指示[教學課程： Windows Azure 儲存體服務中的 SQL Server 資料檔案](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)。  
  
-   *尚未正確建立 SQL Server 認證。*   
    解決方式：請確定您已經針對 [識別] 欄位使用「共用存取簽章」並且正確建立密碼。 檢閱中第 3 課所提供的指示[教學課程： Windows Azure 儲存體服務中的 SQL Server 資料檔案](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)。  
  
 **租用 Blob 錯誤：**  
  
-   在另一個使用相同 Blob 檔案的執行個體已經當機之後，嘗試啟動 SQL Server 時發生錯誤。 解決方式：一般作業期間，SQL Server 會使用暫時租用來保留 Blob 進行儲存，而且每隔 45 至 60 秒就會更新每個 Blob 租用。 如果伺服器當機，而且設定為使用相同 Blob 的另一個 SQL Server 執行個體啟動，新的執行個體最多會等候 60 秒，讓現有的 Blob 租用過期。 如果您想要將資料庫附加至另一個執行個體，而且您無法等候租用在 60 秒內過期，可以明確中斷 Blob 租用，避免附加作業發生任何失敗。  
  
 **資料庫錯誤**  
  
1.  *建立資料庫時發生錯誤*   
    解決方法： 檢閱中第 4 課所提供的指示[教學課程： Windows Azure 儲存體服務中的 SQL Server 資料檔案](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)。  
  
2.  *執行 Alter 陳述式時發生錯誤*   
    解決方式：請務必在資料庫上線時執行 Alter Database 陳述式。 將資料檔案複製到 Windows Azure 儲存體時，一定要建立分頁 Blob 而非區塊 Blob。 否則，ALTER Database 將會失敗。 檢閱中第 7 課所提供的指示[教學課程： Windows Azure 儲存體服務中的 SQL Server 資料檔案](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)。  
  
3.  *錯誤碼 5120 無法開啟實體檔案 "%.\*ls"。作業系統錯誤 %d: "%ls"*   
    解決方式：目前，這項新的增強功能不支援多個 SQL Server 執行個體同時存取 Windows Azure 儲存體中的相同資料庫檔案。 如果 ServerA 在線上且具有作用中的資料庫檔案，而 ServerB 意外啟動，而且也有指向相同資料檔案的資料庫，則第二部伺服器將無法啟動資料庫，錯誤碼為 *5120 無法開啟實體檔案 "%.\*ls"。作業系統錯誤 %d: "%ls"*。  
  
     若要解決此問題，請先判斷您是否需要讓 Server A 存取 Windows Azure 儲存體中的資料庫檔案。 如果不需要，只要移除 Server A 與 Windows Azure 儲存體中資料庫檔案之間的任何連接即可。 若要這樣做，請遵循下列步驟：  
  
    1.  使用 ALTER Database 陳述式，將 Server A 的檔案路徑設定為本機資料夾。  
  
    2.  將 Server A 中的資料庫設為離線。  
  
    3.  然後，將資料庫檔案從 Windows Azure 儲存體複製到 Server A 中的本機資料夾。這樣可確保 Server A 本機仍然具有資料庫的複本。  
  
    4.  將資料庫設為上線。  
  
## <a name="see-also"></a>另請參閱  
 [在 Windows Azure 儲存體服務教學課程： SQL Server 資料檔案](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)  
  
  