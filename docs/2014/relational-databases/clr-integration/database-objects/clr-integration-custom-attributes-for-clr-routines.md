---
title: CLR 常式的自訂屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 817591cec64a4210c4cc573588be1b8ac6dfb8a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62873802"
---
# <a name="custom-attributes-for-clr-routines"></a>CLR 常式的自訂屬性
  列出的屬性可以套用 common language runtime (CLR) 常式、 使用者定義型別，以及在中註冊的使用者定義彙總[!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]。 如果沒有套用屬性，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會假設預設值。 列出的屬性是在 `Microsoft.SqlServer.Server` 命令空間中定義的。  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 屬性  
 `SqlUserDefinedAggregate` 屬性會指出應該將方法註冊為使用者定義彙總。 每個使用者定義彙總都必須使用這個屬性加註。  
  
 如需詳細資訊，請參閱 < [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626)。  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 屬性  
 `SqlFunction` 屬性會利用適當的函數屬性集指出應該將方法註冊為函數。  
  
 如需詳細資訊，請參閱 < [SqlFunctionAttribute](https://go.microsoft.com/fwlink/?LinkId=128019)。  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 屬性  
 `SqlFacet` 屬性用於傳回使用者定義型別 (UDT) 運算式之傳回類型的相關資訊。  
  
 如需詳細資訊，請參閱 < [SqlFacetAttribute](https://go.microsoft.com/fwlink/?LinkId=128020)。  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 屬性  
 `SqlProcedure` 屬性會指出應該將方法註冊為預存程序。 這個屬性只由 Visual Studio 用於自動將指定的方法註冊為預存程序；[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會使用該屬性。  
  
 如需詳細資訊，請參閱 < [SqlProcedureAttribute](https://go.microsoft.com/fwlink/?LinkId=128021)。  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 屬性  
 `SqlTrigger` 屬性會指出應該將方法註冊為觸發程序。  
  
 如需詳細資訊，請參閱 < [SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022)並[SqlTriggerAttribute](https://go.microsoft.com/fwlink/?LinkId=203898)。  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 您可以將 SqlUserDefinedTypeAttribute 套用到組件中的類別定義。 它會使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 建立繫結至包含此自訂屬性之類別定義的使用者定義型別。  
  
 如需詳細資訊，請參閱 < [SqlUserDefinedTypeAttribute](https://go.microsoft.com/fwlink/?LinkId=128024)。  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 屬性  
 `SqlMethod` 屬性用於表示 UDT 之方法或屬性的決定機制和資料存取屬性。  
  
 如需詳細資訊，請參閱 < [SqlMethodAttribute](https://go.microsoft.com/fwlink/?LinkId=128025)。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義彙總](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 使用者定義函式](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 使用者定義型別](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 預存程序](../../../database-engine/dev-guide/clr-stored-procedures.md)   
 [CLR 觸發程序](../../../database-engine/dev-guide/clr-triggers.md)  
  
  
