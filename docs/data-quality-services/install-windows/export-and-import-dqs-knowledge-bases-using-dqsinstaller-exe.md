---
title: 使用 DQSInstaller.exe 匯出及匯入 DQS 知識庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8234c63b-a018-4e55-8184-9a6bdf03274d
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bfbc05c3bc71a0ccac808ebe3b1533bc5d999ddb
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35311387"
---
# <a name="export-and-import-dqs-knowledge-bases-using-dqsinstallerexe"></a>使用 DQSInstaller.exe 匯出及匯入 DQS 知識庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  若為 DQS 的現有安裝，您可以在 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 中將所有知識庫一次匯出到 DQS 備份檔案 (.dqsb)，然後從命令提示字元執行 DQSInstaller.exe 檔案，即可使用此 .dqsb 檔案一次將所有知識庫匯入不同的 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 。 如需有關從命令提示字元執行 DQSInstaller.exe 的詳細資訊，請參閱＜ [從命令提示字元執行 DQSInstaller.exe](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#CommandPrompt) ＞中的＜ [執行 DQSInstaller.exe 完成 Data Quality Server 安裝](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)＞。  
  
 這項功能可讓您在 *中一次備份所有*[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 知識庫，而不必個別使用 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]將每一個知識庫匯出到 .dqs 檔案。 同樣地，您可以從備份檔案一次將所有  知識庫匯入另一個 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] ，而不必使用 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]從 .dqs 檔案個別匯入每一個知識庫。 當您在電腦上解除安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]，然後將它重新安裝在另一部電腦上時，這對於備份和還原知識庫特別有用處。 您可以在現有的 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安裝中輕鬆將所有知識庫匯出到 DQS 備份檔案 (.dqsb)，然後在另一部電腦上安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 之後從備份檔案匯入所有知識庫。  
  
##  <a name="export"></a> 將知識庫匯出到 .dqsb 檔案  
 您可以在任何時間或是解除安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 時，於現有的 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]中匯出所有知識庫。  
  
-   若要在 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 中將所有知識庫匯出到 DQS 備份檔案 (.dqsb)，請從命令提示字元使用 `exportkbs` 參數執行 DQSInstaller.exe，連同您想要匯出知識庫之目標的完整路徑和檔案名稱。 例如，若要將所有知識庫匯出到 C: 磁碟機中的 DQSBackup.dqsb 檔案：  
  
    ```  
    dqsinstaller.exe –exportkbs c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  如果提供的檔案名稱已經存在於指定的位置，安裝程式會提示您是否要覆寫檔案。  
  
-   若要在解除安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]時將所有知識庫匯出到 DQS 備份檔案，請從命令提示字元使用 `uninstall` 參數執行 DQSInstaller.exe，連同您想要匯出知識庫之目標的完整路徑和檔案名稱。 例如，若要將所有知識庫匯出到 C: 磁碟機中的 DQSBackup.dqsb 檔案，然後解除安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]：  
  
    ```  
    dqsinstaller.exe –uninstall c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  如果當您從命令提示字元使用 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 參數解除安裝 `uninstall` 時，並未指定 DQS 備份檔案的完整路徑和檔案名稱，則會顯示一則訊息，表示所有知識庫都將遭到刪除，並可讓您選擇是否要繼續解除安裝程序。  
  
##  <a name="import"></a> 從 .dqsb 檔案匯入知識庫  
 完成 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安裝後，您可以從 DQS 備份檔 (.dqsb) 匯入所有知識庫。 若要匯入知識庫，您必須擁有有效的 DQS 備份檔案 (.dqsb)。  
  
 從命令提示字元使用 `importkbs` 參數執行 DQSInstaller.exe 檔案，連同您想要匯入知識庫之來源的完整路徑和檔案名稱。 例如，若要從 C: 磁碟機中的 DQSBackup.dqsb 檔案匯入所有知識庫：  
  
```  
dqsinstaller.exe –importkbs c:\DQSBackup.dqsb  
```  
  
 如果 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 中目前已經存在與您要匯入的知識庫同名的知識庫，則匯入的知識庫名稱將會附加底線 (_)，後面緊接著以 1 開頭的整數值。 例如，如果 “CompanyName” 定義域是重複的，則匯入的定義域名稱將會是 “CompanyName_1”。  
  
## <a name="see-also"></a>另請參閱  
 [執行 DQSInstaller.exe 完成 Data Quality Server 安裝](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)   
 [安裝 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [將知識庫匯出到 .dqs 檔案](../../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)   
 [從 .dqs 檔案匯入知識](../../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)  
  
  
