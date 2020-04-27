---
title: 從 Microsoft Access 匯入報表（Reporting Services） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Access reports [Reporting Services]
- importing reports
ms.assetid: 4f29d5b8-b77d-4714-a84a-05523df55646
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 862d8b90f3c91dffda35971677db7fdc231c1b63
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108925"
---
# <a name="import-reports-from-microsoft-access-reporting-services"></a>從 Microsoft Access 匯入報表 (Reporting Services)
  在報表設計師中，您可以從[!INCLUDE[msCoName](../includes/msconame-md.md)] Access 資料庫或專案匯入報表。 您必須將 Access 2002 或更新版本安裝在安裝報表設計師的相同電腦上。  
  
 當您使用匯入功能時，會匯入資料庫或專案檔案的所有報表。 如果 Access 檔案包含許多報表，您可以建立個別的報表專案以匯入報表，然後再於主要報表專案中開啟個別的 RDL 檔案。 報表匯入報表設計師之後，就可以編輯報表了。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援所有 Access 報表物件。 未轉換的專案會顯示在 [**工作清單**] 視窗中。 如需詳細資訊，請參閱[支援的存取報告功能 &#40;SSRS&#41;](../../2014/reporting-services/supported-access-report-features-ssrs.md)。  
  
### <a name="to-import-reports-from-microsoft-access"></a>從 Microsoft Access 匯入報表  
  
1.  開啟或建立用來匯入報表的專案。  
  
2.  在 [**專案**] 功能表上，指向 [匯**入報表**]，然後按一下 [ **Microsoft Access**]。 或者，以滑鼠右鍵按一下方案總管中的專案，指向 [匯**入報表**]，然後按一下 [ **Microsoft Access**]。  
  
3.  在 [**開啟**] 對話方塊中，選取包含報表的 Access 資料庫（.mdb、.accdb）或專案（.adp），然後按一下 [**開啟**]。 資料庫或專案檔案中的所有報表都會匯入並列在 [方案總管] 的 [報表] 資料夾中。  
  
4.  檢查 [**工作清單**] 視窗中是否有組建錯誤。 若要查看 [**工作清單**] 視窗，請開啟 [ **view** ] 功能表，指向 [**其他視窗**]，然後按一下 [**工作清單**]。  
  
## <a name="see-also"></a>另請參閱  
 [使用報表設計師設計報表 &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
