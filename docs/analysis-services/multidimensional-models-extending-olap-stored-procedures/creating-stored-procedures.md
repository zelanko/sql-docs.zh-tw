---
title: "建立預存程序 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- registering assemblies
- database assemblies [Analysis Services]
- server assemblies [Analysis Services]
- stored procedures [Analysis Services], creating
- assemblies [Analysis Services]
ms.assetid: a12ff02f-6d0b-4488-9846-3609fc0d0554
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 913b2cbb8fbf93be08b1854051024492e691bdea
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="creating-stored-procedures"></a>建立預存程序
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
所有預存程序都必須與 Common Language Runtime (CLR) 或元件物件模型 (COM) 類別建立關聯，才能使用。 此類別必須安裝在伺服器上 — 通常是在表單的[!INCLUDE[msCoName](../../includes/msconame-md.md)]ActiveX® 動態連結程式庫 (DLL) — 並註冊組件在伺服器上或在為[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。  
  
 預存程序是在伺服器或資料庫上註冊。 可以從任何查詢內容呼叫伺服器預存程序。 只有資料庫內容是為預存程序定義的資料庫時，才能存取資料庫預存程序。 如果某個組件中的函數呼叫其他組件中的函數，您必須將兩個組件註冊在相同內容 (伺服器或資料庫) 中。 針對伺服器或部署[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫的伺服器上，您可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]註冊組件。 如果是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，您可使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 設計師在專案中註冊組件。  
  
> [!IMPORTANT]  
>  COM 組件可能會造成安全性風險。 由於這項風險和其他考量，COM 組件在 [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]中已經被取代。 在未來的版本中，可能不再支援 COM 組件。  
  
## <a name="registering-a-server-assembly"></a>註冊伺服器組件  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，伺服器組件會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體下的 [組件] 資料夾中列出。 伺服器組件可以同時包含 .NET (CLR) 組件與 COM 程式庫。  
  
### <a name="to-create-a-server-assembly"></a>建立伺服器組件  
  
1.  展開執行個體[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]在物件總管 中，以滑鼠右鍵按一下**組件**資料夾，然後再按一下**新組件**。 這會顯示**註冊伺服器組件** 對話方塊。  
  
2.  如**類型**指定組件的類型：  
  
    -   針對 Managed 程式碼 (CLR) DLL，請指定 .NET 組件。  
  
    -   若是機器碼 (COM) DLL，請指定 COM DLL。  
  
3.  如**檔案名稱**，指定包含預存程序的 DLL。  
  
4.  如**組件名稱**，指定組件的名稱。  
  
5.  如果這是偵錯組建的程式庫，您要使用偵錯預存程序，請選取**包含偵錯資訊**核取方塊。 如需有關偵錯預存程序的詳細資訊，請參閱[偵錯預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)。  
  
6.  您可以按一下**確定**立即或在對話方塊工具列上，請註冊組件，您可以按一下命令**指令碼**編寫指令碼來查詢視窗、 檔案或剪貼簿的註冊動作的功能表。  
  
 註冊伺服器組件之後，您可以設定它以滑鼠右鍵按一下 物件總管 中的組件，然後按一下 **屬性**。  
  
## <a name="registering-a-database-assembly-on-the-server"></a>在伺服器上註冊資料庫組件  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，伺服器組件會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫下的 [組件] 資料夾中列出。 資料庫組件可以同時包含 .NET (CLR) 組件和 COM 程式庫。  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>在伺服器上建立資料庫組件  
  
1.  展開執行個體[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫物件總管 中，以滑鼠右鍵按一下**組件**資料夾，然後再按一下**新組件**。 這會顯示**註冊資料庫組件** 對話方塊。  
  
2.  如**類型**指定組件的類型：  
  
    -   針對 Managed 程式碼 (CLR) DLL，請指定 .NET 組件。  
  
    -   若是機器碼 (COM) DLL，請指定 COM DLL。  
  
3.  如**檔案名稱**，指定包含預存程序的 DLL。  
  
4.  如**組件名稱**，指定組件的名稱。  
  
5.  如果這是偵錯組建的程式庫，您要使用偵錯預存程序，請選取**包含偵錯資訊**核取方塊。 如需有關偵錯預存程序的詳細資訊，請參閱[偵錯預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)。  
  
6.  您可以按一下**確定**立即或在對話方塊工具列上，請註冊組件，您可以按一下命令**指令碼**編寫指令碼來查詢視窗、 檔案或剪貼簿的註冊動作的功能表。  
  
 註冊資料庫組件之後，您可以設定它以滑鼠右鍵按一下 物件總管 中的組件，然後按一下 **屬性**。  
  
## <a name="registering-a-database-assembly-in-a-project"></a>在專案中註冊資料庫組件  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的方案總管中，資料庫組件會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案下的 [組件] 資料夾中列出。 資料庫組件可以同時包含 .NET (CLR) 組件和 COM 程式庫。  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>在 Analysis Service 專案中建立資料庫組件  
  
1.  展開執行個體[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫物件總管 中，以滑鼠右鍵按一下**組件**資料夾，然後再按一下**新增組件參考**。 這會顯示**加入參考** 對話方塊。 **.NET**  索引標籤**加入參考**對話方塊會列出現有的.NET (CLR) 組件，而**專案**索引標籤會列出專案。  
  
2.  您可以按一下現有的元件或專案，然後按一下 **新增**將它加入至[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案。 若要新增 COM DLL 的參考，請按一下**瀏覽** 索引標籤來尋找檔案。 **選取的專案和元件**清單會顯示名稱、 類型、 版本，以及每個元件，您要加入至專案的位置。  
  
3.  當您完成選取要加入，請按一下元件**確定**將其新增至[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案。  
  
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
 [多維度模型組件管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定義預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
