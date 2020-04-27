---
title: 建立預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- registering assemblies
- database assemblies [Analysis Services]
- server assemblies [Analysis Services]
- stored procedures [Analysis Services], creating
- assemblies [Analysis Services]
ms.assetid: a12ff02f-6d0b-4488-9846-3609fc0d0554
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7beb77adf595b055a6c1e4a7543b428a06ce7640
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62703084"
---
# <a name="creating-stored-procedures"></a>建立預存程序
  所有預存程序都必須與 Common Language Runtime (CLR) 或元件物件模型 (COM) 類別建立關聯，才能使用。 類別必須安裝在伺服器上-通常是以[!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX®動態連結程式庫（DLL）的形式，並在伺服器或[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫中註冊為元件。  
  
 預存程序是在伺服器或資料庫上註冊。 可以從任何查詢內容呼叫伺服器預存程序。 只有資料庫內容是為預存程序定義的資料庫時，才能存取資料庫預存程序。 如果某個組件中的函數呼叫其他組件中的函數，您必須將兩個組件註冊在相同內容 (伺服器或資料庫) 中。 如果是伺服器或伺服器上[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]已部署的資料庫，您可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來註冊元件。 如果是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，您可使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 設計師在專案中註冊組件。  
  
> [!IMPORTANT]  
>  COM 組件可能會造成安全性風險。 由於這項風險和其他考量，COM 組件在 [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]中已經被取代。 在未來的版本中，可能不再支援 COM 組件。  
  
## <a name="registering-a-server-assembly"></a>註冊伺服器組件  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，伺服器組件會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體下的 [組件] 資料夾中列出。 伺服器組件可以同時包含 .NET (CLR) 組件與 COM 程式庫。  
  
### <a name="to-create-a-server-assembly"></a>建立伺服器組件  
  
1.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在物件總管中展開的實例，以滑鼠右鍵按一下 [**元件**] 資料夾，然後按一下 [**新增元件**]。 這會顯示 [**註冊伺服器元件**] 對話方塊。  
  
2.  針對 [**類型**]，指定元件的類型：  
  
    -   針對 Managed 程式碼 (CLR) DLL，請指定 .NET 組件。  
  
    -   若是機器碼 (COM) DLL，請指定 COM DLL。  
  
3.  針對 [**檔案名**]，指定包含預存程式的 DLL。  
  
4.  針對 [**元件名稱**]，指定元件的名稱。  
  
5.  如果這是您要用來進行預存程式之程式庫的偵錯工具組建，請選取 [**包含 debug 資訊**] 核取方塊。 如需有關偵錯工具預存程式的詳細資訊，請參閱[偵錯工具預存程式](debugging-stored-procedures.md)。  
  
6.  您可以按一下 **[確定]** 立即註冊元件，或在對話方塊工具列上，按一下 [**腳本**] 功能表上的命令，將註冊動作的腳本編寫為查詢視窗、檔案或剪貼簿。  
  
 註冊伺服器元件之後，您可以在物件總管中的元件上按一下滑鼠右鍵，然後按一下 [**屬性**] 來設定它。  
  
## <a name="registering-a-database-assembly-on-the-server"></a>在伺服器上註冊資料庫組件  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，伺服器組件會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫下的 [組件] 資料夾中列出。 資料庫組件可以同時包含 .NET (CLR) 組件和 COM 程式庫。  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>在伺服器上建立資料庫組件  
  
1.  在 [物件總管中[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]展開資料庫的實例，以滑鼠右鍵按一下 [**元件**] 資料夾，然後按一下 [**新增元件**]。 這會顯示 [**註冊資料庫元件**] 對話方塊。  
  
2.  針對 [**類型**]，指定元件的類型：  
  
    -   針對 Managed 程式碼 (CLR) DLL，請指定 .NET 組件。  
  
    -   若是機器碼 (COM) DLL，請指定 COM DLL。  
  
3.  針對 [**檔案名**]，指定包含預存程式的 DLL。  
  
4.  針對 [**元件名稱**]，指定元件的名稱。  
  
5.  如果這是您要用來進行預存程式之程式庫的偵錯工具組建，請選取 [**包含 debug 資訊**] 核取方塊。 如需有關偵錯工具預存程式的詳細資訊，請參閱[偵錯工具預存程式](debugging-stored-procedures.md)。  
  
6.  您可以按一下 **[確定]** 立即註冊元件，或在對話方塊工具列上，按一下 [**腳本**] 功能表上的命令，將註冊動作的腳本編寫為查詢視窗、檔案或剪貼簿。  
  
 註冊資料庫元件之後，您可以在物件總管中的元件上按一下滑鼠右鍵，然後按一下 [**屬性**] 來設定它。  
  
## <a name="registering-a-database-assembly-in-a-project"></a>在專案中註冊資料庫組件  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的方案總管中，資料庫組件會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案下的 [組件] 資料夾中列出。 資料庫組件可以同時包含 .NET (CLR) 組件和 COM 程式庫。  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>在 Analysis Service 專案中建立資料庫組件  
  
1.  在 [物件總管中[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]展開資料庫的實例，以滑鼠右鍵按一下 [**元件**] 資料夾，然後按一下 [**新增元件參考**]。 這會顯示 [**加入參考**] 對話方塊。 [**加入參考**] 對話方塊的 [ **.net** ] 索引標籤會列出現有的 .net （CLR）元件，而 [**專案**] 索引標籤則會列出專案。  
  
2.  您可以按一下現有的元件或專案，然後按一下**Add** [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]新增] 將它加入至專案。 若要加入 COM DLL 的參考，請按一下 [**流覽**] 索引標籤來尋找檔案。 [**選取的專案和元件**] 清單會顯示您要新增至專案之每個元件的名稱、類型、版本和位置。  
  
3.  當您完成選取要加入的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]元件時，請按一下 **[確定]** 將其新增至專案。  
  
## <a name="script-format-for-an-assembly"></a>組件的指令碼格式  
 註冊 .NET 組件相當地簡單。 .NET 組件會使用下列格式，以二進位格式加入資料庫中：  
  
```  
<Create>  
   <ObjectDefinition>  
      <Assembly>  
         <Files>  
            <File>  
               <Name>filename</Name>  
               <Type>filetype</Type>  
               <Data>  
                  <Block>binarydatablock</Block>  
                  <Block>binarydatablock</Block>  
                  ...  
               </Data>  
            </File>  
         </Files>  
         <PermissionSet>PermissionSet</PermissionSet>  
      </Assembly>  
   <ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型元件管理](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定義預存程序](defining-stored-procedures.md)  
  
  
