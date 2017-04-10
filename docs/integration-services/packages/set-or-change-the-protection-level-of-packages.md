---
title: "設定或變更封裝的保護等級 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "密碼 [Integration Services]"
  - "封裝 [Integration Services], 安全性"
  - "安全性 [Integration Services], 保護等級"
  - "封裝的保護等級 [Integration Services]"
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# 設定或變更封裝的保護等級
  若要控制封裝內容以及其中包含之機密值 (例如密碼) 的存取權，請設定 **ProtectionLevel** 屬性的值。 包含在專案中的封裝需要有和專案相同的保護層級，才能建立專案。 如果您變更專案上的 **ProtectionLevel** 屬性設定，就需要手動更新封裝的屬性設定。  
  
 如需如何在封裝生命週期不同階段，判斷適用於您的封裝之 **ProtectionLevel** 設定的詳細資訊，請參閱[封裝中的敏感性資料存取控制](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)。 如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 安全性功能的概觀，請參閱[安全性概觀 &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)。  
  
 本主題中的程序說明如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 dtutil 命令提示字元公用程式來變更 **ProtectionLevel** 屬性。  
  
> [!NOTE]  
>  除了本主題中的程序之外，您通常可以在匯入或匯出封裝時，設定或變更封裝的 **ProtectionLevel** 屬性。 您也可以在使用 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 來儲存封裝時，變更封裝的 **ProtectionLevel** 屬性。  
  
### 若要在 SQL Server 資料工具中設定或變更封裝的保護等級  
  
1.  在[設定封裝的保護等級](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)主題中，檢閱 **ProtectionLevel** 屬性可用的值，並判斷適用於您的封裝的值。  
  
2.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，開啟包含封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計器中，開啟封裝。  
  
4.  如果 [屬性] 視窗並未顯示封裝屬性，請按一下設計介面。  
  
5.  在 [屬性] 視窗的 [安全性] 群組中，為 **ProtectionLevel** 屬性選取適當的值。  
  
     如果您選取了需要密碼的保護等級，請輸入密碼作為 **PackagePassword** 屬性的值。  
  
6.  在 [檔案] 功能表上，選取 [儲存選取項目] 以儲存修改過的封裝。  
  
### 在命令提示字元設定或變更封裝的保護等級  
  
1.  在[設定封裝的保護等級](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)主題中，檢閱 **ProtectionLevel** 屬性可用的值，並判斷適用於您的封裝的值。  
  
2.  在 [dtutil 公用程式](../../integration-services/dtutil-utility.md)主題中，檢閱 **Encrypt** 選項的對應，並判斷適合當做所選 **ProtectionLevel** 屬性值的整數。  
  
3.  開啟 [命令提示字元] 視窗。  
  
4.  在命令提示字元，導覽至您要設定其 **ProtectionLevel** 屬性之封裝的所在資料夾。  
  
     下列步驟所示的語法範例假設此資料夾為目前的資料夾。  
  
5.  使用類似於下列其中一個範例的命令，設定或變更封裝的保護等級：  
  
    -   下列命令會將檔案系統中個別封裝的 **ProtectionLevel** 屬性設為層級 2「機密資料以密碼加密」，並且將密碼設為 "strongpassword"：  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   下列命令會將檔案系統中特定資料夾內所有封裝的 **ProtectionLevel** 屬性設為層級 2「機密資料以密碼加密」，並且將密碼設為 "strongpassword"：  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         如果您要對批次檔使用類似命令，請將檔案預留位置 "%f" 改輸入為批次檔適用的 "%%f"。  
  
## 請參閱＜  
 [dtutil 公用程式](../../integration-services/dtutil-utility.md)  
  
  