---
description: MSSQLSERVER_8632
title: MSSQLSERVER_8632
ms.custom: ''
ms.date: 10/27/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8632 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 36f8b6f7eb55a30becf0f56eb318c6740b5783ec
ms.sourcegitcommit: f87f2f0f1edc91fe400040d8e3a5810347aa8d70
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2020
ms.locfileid: "96868898"
---
# <a name="mssqlserver_8632"></a>MSSQLSERVER_8632
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細資料

|屬性|值|
|---|---|
|產品名稱|SQL Server|
|事件識別碼|8632|
|事件來源|MSSQLSERVER|
|元件|SQLEngine|
|符號名稱|QUERY_EXPRESSION_TOO_COMPLEX|
|訊息文字|內部錯誤：到達運算式服務的限制。 請找出查詢中潛在的複雜運算式，並嘗試加以簡化。|
||

## <a name="explanation"></a>說明

當您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行查詢，且其中有單一運算式包含大量的識別碼和常數，就會引發錯誤 8632。 使用者會收到類似下列的錯誤訊息回報：

> 伺服器：訊息 8632，層級 17，狀態 2，第 1 行  
內部錯誤：到達運算式服務的限制。 請找出查詢中潛在的複雜運算式，並嘗試加以簡化。

## <a name="cause"></a>原因

發生這個問題的原因是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會限制查詢的單一運算式中可包含的識別碼和常數個數。 此限制為 65,535。 例如，下列查詢只有一個運算式：

```sql
select a, b + c, d + e
```

此運算式會擷取所有五個資料行、計算加法運算子，並將三個預計的結果傳送至用戶端。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 展開所有參考的識別碼和常數之後，就會對識別碼和常數的個數進行測試。 例如，可能會展開下列項目：

- 選取清單中的星號 (*)
- 檢視
- 計算資料行定義

如果展開後的個數超過限制，則無法執行查詢。

## <a name="user-action"></a>使用者動作

若要解決此問題，請重寫您的查詢。 請在查詢的最大運算式中參考較少的識別碼和常數。 您必須確保查詢中所有運算式的識別碼和常數個數均不會超過限制。 若要這麼做，您可能必須將查詢分解成多個單一查詢。 然後，建立暫時的中繼結果。
