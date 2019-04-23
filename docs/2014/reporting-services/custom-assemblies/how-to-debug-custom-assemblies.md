---
title: HOW TO：偵錯自訂組件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom assemblies [Reporting Services], debugging
- debugging custom assemblies [Reporting Services]
- troubleshooting [Reporting Services], custom assemblies
ms.assetid: 3a3215b3-548c-4474-81ba-3a98dd3912bf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 64a61e044c7ff6efe051eb316cb9f653f0993b68
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "60154194"
---
# <a name="how-to-debug-custom-assemblies"></a>HOW TO：針對自訂組件進行偵錯
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 提供數個偵錯工具，可協助您分析自訂組譯碼並尋找其中的錯誤。 要使用的最佳工具將視您嘗試完成的項目而定。 此範例會使用 [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]。  
  
 設計、開發和測試 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 自訂組件的建議方法，是建立包含測試報表與自訂組件的方案。  
  
### <a name="to-debug-assemblies-using-a-single-instance-of-visual-studio"></a>若要使用 Visual Studio 的單一執行個體偵錯組件  
  
1.  使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 建立新報表專案。  
  
     在建立報表專案時，[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 也會建立一個包含該專案的方案。  
  
2.  將新的類別庫專案加入現有的方案中。 請確定將報表專案設定為啟動專案。 如需有關如何完成這項動作的詳細資訊，請參閱您的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 文件集。  
  
3.  在 [方案總管] 中，選取方案。  
  
4.  在 [檢視] 功能表上按一下 [屬性頁]。  
  
     [方案屬性頁] 對話方塊隨即開啟。  
  
5.  在左窗格中，若有需要，請展開 [通用屬性]，然後按一下 [專案相依性]。 從 [專案] 下拉式清單中，選取報表專案。 在 [相依於] 清單中選取組件專案。  
  
6.  按一下 [確定] 儲存變更，然後關閉 [屬性頁] 對話方塊。  
  
7.  在 [方案總管] 中，選取自訂組件專案。  
  
8.  在 [檢視] 功能表上按一下 [屬性頁]。  
  
     [專案屬性頁] 對話方塊隨即開啟。  
  
9. 按一下 [建立] 索引標籤 (如果您在 C# 專案中) 或 [編譯] 索引標籤 (如果您在 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 專案中)。  
  
10. 在 [建立]/[編譯] 頁面上，輸入報表設計師資料夾的路徑。 根據預設，這是 [輸出路徑] 文字方塊中的 C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE)。 這將會在執行報表之前，建立自訂組件的更新版本並將它直接部署到報表設計師。  
  
11. 一旦您已設計報表並開發自訂組件，請在自訂組件程式碼中設定中斷點。  
  
12. 請按 F5 鍵在 **DebugLocal** 模式之下執行報表。 當報表在快顯預覽視窗中執行時，偵錯程式會叫用任何對應至組件中可執行的程式碼之中斷點。 使用 F11 逐步完成自訂組件程式碼。  
  
### <a name="to-debug-assemblies-using-two-instances-of-visual-studio"></a>若要使用 Visual Studio 的兩個執行個體偵錯組件  
  
1.  啟動 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，然後開啟自訂組件專案。  
  
2.  建立專案，然後將自訂組件與隨附的 .pdb 檔案部署到報表設計師。 如需部署的詳細資訊，請參閱[部署自訂組件](deploying-a-custom-assembly.md)。  
  
3.  開啟使用自訂組件的報表專案，同時在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 的個別執行個體中，將自訂組件程式碼保持在開啟的狀態。  
  
4.  導覽到包含自訂組件專案的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 執行個體，並在程式碼中設定某些中斷點。  
  
5.  當自訂組件專案仍為使用中視窗時，按一下 [偵錯] 功能表上的 [附加至處理序]。  
  
     [附加至處理序] 對話方塊隨即開啟。  
  
6.  從處理序清單中，選取對應至報表專案的 devenv.exe 處理序，然後按一下 [附加]。  
  
7.  定義在報表中將從自訂組件使用的運算式，並設計報表。  
  
8.  當您完成設計報表時，請按一下 [預覽] 索引標籤。  
  
     報表會執行，而且自訂組件程式碼應該在預先定義的中斷點中斷。  
  
    > [!NOTE]  
    >  使用 [預覽] 索引標籤並不會強制組件的程式碼權限。 如需包括任何程式碼存取安全性錯誤的完整測試，請在 **DebugLocal** 組態設定之下啟動報表專案。  
  
9. 使用 F11 鍵逐步執行程式碼。 如需有關使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 來偵錯的詳細資訊，請參閱 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [將自訂組件與報表搭配使用](using-custom-assemblies-with-reports.md)  
  
  
