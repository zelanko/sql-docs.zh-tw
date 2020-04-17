---
title: CLR 例程的自訂屬性 |微軟文件
description: 自訂屬性可以應用於在 Microsoft SQL Server 中註冊的 CLR 例程、使用者定義的類型和使用者定義的聚合。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
ms.openlocfilehash: a32a606f73858ede15569d1ade891ad2ce1c69a5
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487936"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>CLR 常式的 CLR 整合自訂屬性
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  列出的屬性可以應用於在中[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]註冊的常見語言運行時 (CLR) 例程、使用者定義的類型和使用者定義的聚合。 如果沒有套用屬性，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會假設預設值。 列出的屬性在**Microsoft.SqlServer.Server.Server**命名空間中定義。  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 屬性  
 **SqlUser 定義聚合**屬性指示該方法應註冊為使用者定義的聚合。 每個使用者定義彙總都必須使用這個屬性加註。  
  
 有關詳細資訊,請參閱[SqlUser 定義的集合屬性](https://go.microsoft.com/fwlink/?LinkId=124626)。  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 屬性  
 **SqlFunction**屬性指示該方法應註冊為函數,並設置相應的函數屬性。  
  
 有關詳細資訊,請參閱[SqlFunction 屬性](https://go.microsoft.com/fwlink/?LinkId=128019)。  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 屬性  
 **SqlFacet**屬性用於返回有關使用者定義類型 (UDT) 運算式傳回類型的資訊。  
  
 有關詳細資訊,請參閱[SqlFacet 屬性](https://go.microsoft.com/fwlink/?LinkId=128020)。  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 屬性  
 **Sql程序**屬性指示該方法應註冊為存儲過程。 這個屬性只由 Visual Studio 用於自動將指定的方法註冊為預存程序；[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會使用該屬性。  
  
 有關詳細資訊,請參閱[Sql 程式屬性](https://go.microsoft.com/fwlink/?LinkId=128021)。  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 屬性  
 **SqlTrigger**屬性指示該方法應註冊為觸發器。  
  
 有關詳細資訊,請參閱[SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022)和[SqlTrigger 屬性](https://go.microsoft.com/fwlink/?LinkId=203898)。  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 您可以將 SqlUserDefinedTypeAttribute 套用到組件中的類別定義。 它會使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 建立繫結至包含此自訂屬性之類別定義的使用者定義型別。  
  
 有關詳細資訊,請參閱[SqlUser 定義類型屬性](https://go.microsoft.com/fwlink/?LinkId=128024)。  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 屬性  
 **SqlMethod**屬性用於指示方法或 UDT 上屬性的確定性和數據訪問屬性。  
  
 有關詳細資訊,請參閱[SqlMethodattribute](https://go.microsoft.com/fwlink/?LinkId=128025)。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義的集合合](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 使用者定義的函數](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 使用者定義類型](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 預存程序](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [CLR 觸發程序](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
