---
title: 資料集屬性對話方塊、 選項 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10130"
- sql12.rtp.rptdesigner.datasetproperties.options.f1
ms.assetid: 95299049-71ba-427f-b723-775cb696243f
caps.latest.revision: 39
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7018038707462c2cf32a733b31cf66d25a275bfb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319738"
---
# <a name="dataset-properties-dialog-box-options"></a>資料集屬性對話方塊、選項
  選取 **選項**上**資料集屬性**對話方塊來變更資料的選項，例如定序選項和小計的查詢。 如需詳細資訊，請參閱 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="options"></a>選項。  
 **定序**  
 選取決定排序資料所用之定序順序的地區設定。 **[預設值]** 指出報表伺服器應該在報表執行時，嘗試從資料提供者衍生此值。 如果無法衍生此值，則從電腦的地區設定衍生預設值。  
  
 **區分大小寫**  
 選取決定區分大小寫的值。 此選項指出資料是否區分大小寫。 您可以將 **[區分大小寫]** 設定為 **[True]**、 **[False]** 或 **[Auto]**。預設值 [Auto] 指出報表伺服器應該在報表執行時，嘗試從資料提供者衍生此值。 如果資料提供者不支援區分大小寫類型，報表會以該值為 **False**來執行。 如果您知道值，而且知道系統支援該值，選擇 **[True]**。  
  
 **區分腔調字**  
 選取決定區分腔調字的值。 **[區分腔調字]** 指出資料是否區分腔調字，而且可以設定為 **[True]**、 **[False]** 或 **[Auto]**。預設值 [Auto] 指出報表伺服器應該在報表執行時，嘗試從資料提供者衍生此值。 如果資料提供者不支援區分腔調字類型，報表會以該值為 **[False]** 來執行。 如果您知道值，而且知道系統支援該值，選擇 **[True]**。  
  
 **區分假名**  
 選取決定區分假名的值。 此選項指出資料是否區分假名；它可以設定為 **[True]**、 **[False]** 或 **[Auto]**。預設值 [Auto] 指出報表伺服器應該在報表執行時，嘗試從資料提供者衍生此值。 如果資料提供者不支援區分假名類型，報表會以該值為 **[False]** 來執行。 如果您知道值，而且知道系統支援該值，選擇 **[True]**。  
  
 **區分全半形**  
 選取決定區分全半形的值。 此選項指出資料是否區分全半形，而且可以設定為 **True**、 **False**或 **Auto**。預設值 [Auto] 指出報表伺服器應該在報表執行時，嘗試從資料提供者衍生此值。 如果資料提供者不支援區分全半形類型，報表會以該值為 **[False]** 來執行。 如果您知道值，而且知道系統支援該值，選擇 **[True]**。  
  
 **將小計當做詳細資料列**  
 選取一個值，指出您是否要讓小計資料列當做詳細資料列而非彙總資料列。 預設值**自動**，表示將小計資料列應視為詳細資料列是否報表不使用`Aggregate`（） 函式，來存取資料集中的任何欄位。 如果您要讓小計資料列當做彙總資料列，選擇 **[False]**。 如果您想解譯為詳細資料列的小計資料列，而且您知道它們不使用`Aggregate`（) 函式中，選擇 **，則為 True**。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表或文字方塊的地區設定&#40;Reporting Services&#41;](report-design/set-the-locale-for-a-report-or-text-box-reporting-services.md)   
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Windows 定序名稱 &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [SQL Server 定序名稱 &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [彙總函式&#40;報表產生器及 SSRS&#41;](report-design/report-builder-functions-aggregate-function.md)  
  
  
