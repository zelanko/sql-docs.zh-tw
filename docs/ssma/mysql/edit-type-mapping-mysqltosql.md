---
description: 編輯類型對應 (MySQLToSQL)
title: 編輯類型對應 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 184f7ab2-725f-491e-a15b-b889f2fb6a68
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7dc968e4e9bd2d33c4a15de625f5abd12a3696a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492450"
---
# <a name="edit-type-mapping-mysqltosql"></a>編輯類型對應 (MySQLToSQL)
[ **編輯類型對應** ] 對話方塊可讓您指定如何在來源與目的地資料庫物件之間對應類型。  
  
您可以在幾個地方存取此對話方塊：  
  
-   當您選取源資料庫或資料庫物件時，[ **類型對應** ] 索引標籤會出現在中繼資料瀏覽器的右邊。 按一下 [ **加入** ] 以加入新的型別對應，或按一下 [ **編輯** ] 來變更現有的型別對應。  
  
-   在 [ **工具** ] 功能表上，選取 [ **專案設定** ] 或 [ **預設專案設定**]。 在 [產生的] 對話方塊中，選取 [ **類型對應**]。 按一下 [ **加入** ] 以加入新的型別對應，或按一下 [ **編輯** ] 來變更現有的型別對應。  
  
-   資料表特定的類型對應會覆寫資料庫和專案類型對應。 資料庫特定對應會覆寫專案對應。  
  
## <a name="options"></a>選項。  
  
##### <a name="source-type"></a>來源類型  
選取要對應至 SQL Server 資料類型的源資料類型。  
  
如果資料類型的長度是可變的，則下欄欄位會出現在 [ **Sourcetype**] 下方：  
  
##### <a name="from"></a>寄件者  
指定此對應的最小長度。 例如，針對**Nchar**資料類型，您可以輸入10以指定此對應是針對從**Nchar (10) **開始的範圍。  
  
##### <a name="to"></a>收件者  
指定此對應的最大長度。 例如，針對 **Nchar** 資料類型，您可以輸入20以指定此對應的範圍結束于 **Nchar (20) 。**  
  
##### <a name="target-type"></a>目標類型  
選取源資料類型所對應的 SQL Server 資料類型。 當 SSMA 建立資料表或 SQL Server 中，源資料類型會變更為此資料類型。  
  
如果資料類型的長度為可變，則下欄欄位會出現在 [ **目標型別**] 下方：  
  
##### <a name="replace-with"></a>更換為  
指定此對應的目標長度。 例如，對於 **Nvarchar** 資料類型，您可以輸入20以指定指定的源資料類型應該對應至 **Nvarchar (20) 。**  
  
