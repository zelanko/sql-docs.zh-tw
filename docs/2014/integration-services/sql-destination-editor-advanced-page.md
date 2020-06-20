---
title: SQL 目的地編輯器（Advanced Page） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 9b46bcf8-ddaf-4d7d-90a6-80bc19517e9b
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d7a3cdc57f48c61894a51386c5671c98e00ba711
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962709"
---
# <a name="sql-destination-editor-advanced-page"></a>SQL 目的地編輯器 (進階頁面)
  使用 [SQL 目的地編輯器]**** 對話方塊的 [進階]**** 頁面，即可指定進階大量插入選項。  
  
 若要深入了解 SQL Server 目的地，請參閱＜ [SQL Server Destination](data-flow/sql-server-destination.md)＞。  
  
## <a name="options"></a>選項。  
 **保留識別**  
 指定工作是否應該將值插入識別欄位中。 此屬性的預設值為 `False`。  
  
 **保留 Null**  
 指定工作是否應該保留 Null 值。 此屬性的預設值為 `False`。  
  
 **表鎖**  
 指定載入資料時是否鎖定資料表。 此屬性的預設值為 `True`。  
  
 **檢查條件約束**  
 指定工作是否應該檢查條件約束。 此屬性的預設值為 `True`。  
  
 **引發觸發程序**  
 指定大量插入是否應該引發資料表上的觸發程序。 此屬性的預設值為 `False`。  
  
 **第一個資料列**  
 指定要插入的第一個資料列。 這個屬性的預設值為 **-1**，表示未指派任何值。  
  
> [!NOTE]  
>  清除 [SQL 目的地編輯器]**** 中的文字方塊，以指出您不要指派此屬性的值。 在 [屬性]**** 視窗、[進階編輯器]**** 和物件模型中，請使用 -1。  
  
 **最後一個資料列**  
 指定要插入的最後一個資料列。 這個屬性的預設值為 **-1**，表示未指派任何值。  
  
> [!NOTE]  
>  清除 [SQL 目的地編輯器]**** 中的文字方塊，以指出您不要指派此屬性的值。 在 [屬性]**** 視窗、[進階編輯器]**** 和物件模型中，請使用 -1。  
  
 **錯誤數目上限**  
 指定停止大量插入之前可以發生的錯誤數目。 這個屬性的預設值為 **-1**，表示未指派任何值。  
  
> [!NOTE]  
>  清除 [SQL 目的地編輯器]**** 中的文字方塊，以指出您不要指派此屬性的值。 在 [屬性]**** 視窗、[進階編輯器]**** 和物件模型中，請使用 -1。  
  
 **逾時**  
 指定因逾時而停止大量插入之前要等候的秒數。  
  
 **排序資料行**  
 輸入排序資料行的名稱。 每個資料行都可依遞增或遞減順序來排序。 如果您使用多個排序資料行，請用逗號分隔此清單。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL 目的地編輯器 &#40;連線管理員頁面&#41;](../../2014/integration-services/sql-destination-editor-connection-manager-page.md)   
 [[SQL 目的地編輯器 &#40;對應] 頁面&#41;](../../2014/integration-services/sql-destination-editor-mappings-page.md)   
 [使用 SQL Server 目的地來大量載入資料](data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
