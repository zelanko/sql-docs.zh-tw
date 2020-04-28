---
title: 編輯類型對應（MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 184f7ab2-725f-491e-a15b-b889f2fb6a68
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d31304dae7246e425ef54af6d1382af7e885696c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103004"
---
# <a name="edit-type-mapping-mysqltosql"></a>編輯類型對應 (MySQLToSQL)
[**編輯類型對應**] 對話方塊可讓您指定如何在來源與目的地資料庫物件之間對應類型。  
  
您可以在數個位置存取此對話方塊：  
  
-   當您選取源資料庫或資料庫物件時，[**類型對應**] 索引標籤會出現在 [中繼資料] explorer 的右邊。 按一下 [**加入**] 以加入新的類型對應，或按一下 [**編輯**] 以變更現有的類型對應。  
  
-   在 [**工具**] 功能表上，選取 [**專案設定**] 或 [**預設專案設定**]。 在產生的對話方塊中，選取 [**類型對應**]。 按一下 [**加入**] 以加入新的類型對應，或按一下 [**編輯**] 以變更現有的類型對應。  
  
-   資料表特定類型對應會覆寫資料庫和專案類型對應。 資料庫特定對應會覆寫專案對應。  
  
## <a name="options"></a>選項  
  
##### <a name="source-type"></a>來源類型  
選取要對應至 SQL Server 資料類型的源資料類型。  
  
如果資料類型的長度可變，下欄欄位會出現在 [ **Sourcetype**] 底下：  
  
##### <a name="from"></a>從  
指定此對應的最小長度。 例如，針對**Nchar**資料類型，您可以輸入10來指定此對應是針對從**Nchar （10）** 開始的範圍。  
  
##### <a name="to"></a>至  
指定此對應的最大長度。 例如，針對**Nchar**資料類型，您可以輸入20來指定此對應是針對結束于**Nchar （20）** 的範圍。  
  
##### <a name="target-type"></a>目標類型  
選取源資料類型所對應的 SQL Server 資料類型。 當 SSMA 在 SQL Server 建立資料表或時，源資料類型將會變更為此資料類型。  
  
如果資料類型是可變長度，下欄欄位會出現在 [**目標型別**] 底下：  
  
##### <a name="replace-with"></a>更換為  
指定此對應的目標長度。 例如，針對**Nvarchar**資料類型，您可以輸入20，指定指定的源資料類型應對應至**Nvarchar （20）。**  
  
