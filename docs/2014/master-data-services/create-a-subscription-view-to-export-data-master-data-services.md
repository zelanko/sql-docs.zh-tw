---
title: 建立訂閱檢視(主資料服務) |微軟文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c4a2f747192b1cddefeac256d4470a2b345305de
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "65479941"
---
# <a name="create-a-subscription-view-master-data-services"></a>建立訂閱檢視 (Master Data Services)
  如果要在[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]資料庫中創建數據檢視,以便訂閱系統使用,請創建訂閱檢視。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[整合管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 有關詳細資訊,請參閱[管理員&#40;主資料服務&#41;](administrators-master-data-services.md)。  
  
### <a name="to-create-a-subscription-view"></a>若要建立訂閱檢視  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，按一下 **[整合管理]**。  
  
2.  按一下功能表列上的 **[建立檢視表]**。  
  
3.  在 **「訂閱檢視」** 頁上,按下「**新增訂閱」 檢視**。  
  
4.  在 **「創建訂閱檢視」** 窗格中,在 **「訂閱檢視」 名稱**框中鍵入檢視的名稱。  
  
5.  從 **[模型]** 清單中選取模型。  
  
6.  選擇**版本**「或 **」版本標誌」** 選項,然後從相應的清單中選擇。  
  
    > [!TIP]  
    >  根據版本旗標建立訂閱檢視。 當您鎖定版本時，您可以重新指派旗標給開啟的版本，而不用更新訂閱檢視。  
  
7.  選擇 **「實體**」或「**派生」層次結構**選項,然後從相應的清單中選擇。  
  
8.  從 **[格式]** 清單中選取訂閱檢視格式。  
  
9. 如果您從 **[格式]** 清單中選擇 **[明確層級]** 或 **[衍生層級]** ，請輸入階層內要加入檢視中的層級數。  
  
10. 按一下 [檔案]  。  
  
## <a name="see-also"></a>另請參閱  
 [匯出資料&#40;主資料服務&#41;](overview-exporting-data-master-data-services.md)   
 [刪除訂閱檢視&#40;主資料服務&#41;](delete-a-subscription-view-master-data-services.md)   
 [建立版本旗標 &#40;Master Data Services&#41;](create-a-version-flag-master-data-services.md)  
  
  
