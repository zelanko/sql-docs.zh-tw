---
title: 自訂應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ab470951162b5e4035c1253ed4ce425356ad8ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799856"
---
# <a name="custom-applications"></a>自訂應用程式
自訂應用程式通常會執行特定工作的幾個 Dbms。 例如，應用程式可能會擷取單一的 DBMS 資料和產生報表，或它可能會傳送數個 Dbms 之間的資料。 這些應用程式怎麼在一般是這些 Dbms 寫入應用程式之前，先已知，且不太可能會變更應用程式生命週期。  
  
 自訂的應用程式因此需要幾乎沒有任何互通性。 應用程式開發人員可以選擇一個驅動程式，針對每個 DBMS 和直接向這些驅動程式的程式碼。 應用程式可以安全地包含驅動程式專屬程式碼，來利用這些驅動程式的功能，而且甚至可能讓原生資料庫 API 呼叫使用不支援 ODBC 的功能。  
  
 大部分的自訂應用程式的主要的互通性考量為是否目標 Dbms 會在未來變更。 如果是的話，可簡化此程序開始撰寫更具互通性的程式碼。 不過，這類變更的 Dbms 很少見，而且通常需要大量的工作。 因此，自訂的應用程式開發人員很少選擇增加互通性，但會犧牲功能;它們通常會選擇來變更 Dbms 時，重新設定該功能。
