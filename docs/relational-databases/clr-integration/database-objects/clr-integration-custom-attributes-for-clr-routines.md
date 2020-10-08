---
title: CLR 常式的自訂屬性 |Microsoft Docs
description: 自訂屬性可以套用至 CLR 常式、使用者定義型別，以及在 Microsoft SQL Server 中註冊的使用者定義匯總。
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
ms.openlocfilehash: bad209c4ddb516167b8048ae73680bc9ea59cc05
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810802"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>CLR 常式的 CLR 整合自訂屬性
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  列出的屬性可以套用至 common language runtime (CLR) 常式、使用者定義型別，以及在中註冊的使用者定義匯總 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 如果沒有套用屬性，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會假設預設值。 列出的屬性會定義于 **Microsoft SqlServer. 伺服器** 命名空間中。  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 屬性  
 **SqlUserDefinedAggregate**屬性會指出應該將方法註冊為使用者定義匯總。 每個使用者定義彙總都必須使用這個屬性加註。  
  
 如需詳細資訊，請參閱 [SqlUserDefinedAggregateAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedaggregateattribute)。  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 屬性  
 **SqlFunction**屬性指出應該將方法註冊為函數，並設定適當的函式屬性。  
  
 如需詳細資訊，請參閱 [SqlFunctionAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfunctionattribute)。  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 屬性  
 **SqlFacet**屬性是用來傳回使用者定義型別的傳回型別相關資訊 (UDT) 運算式。  
  
 如需詳細資訊，請參閱 [SqlFacetAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfacetattribute)。  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 屬性  
 **SqlProcedure**屬性指出應該將方法註冊為預存程式。 這個屬性只由 Visual Studio 用於自動將指定的方法註冊為預存程序；[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會使用該屬性。  
  
 如需詳細資訊，請參閱 [SqlProcedureAttribute](/dotnet/api/microsoft.sqlserver.server.sqlprocedureattribute)。  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 屬性  
 **SqlTrigger**屬性指出應該將方法註冊為觸發程式。  
  
 如需詳細資訊，請參閱 [SqlTriggerCoNtext](/dotnet/api/microsoft.sqlserver.server.sqltriggercontext) 和 [SqlTriggerAttribute](/dotnet/api/microsoft.sqlserver.server.sqltriggerattribute)。  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 您可以將 SqlUserDefinedTypeAttribute 套用到組件中的類別定義。 它會使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 建立繫結至包含此自訂屬性之類別定義的使用者定義型別。  
  
 如需詳細資訊，請參閱 [SqlUserDefinedTypeAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedtypeattribute)。  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 屬性  
 **SqlMethod**屬性是用來指出方法的確定性和資料存取屬性，或是 UDT 的屬性。  
  
 如需詳細資訊，請參閱 [SqlMethodAttribute](/dotnet/api/microsoft.sqlserver.server.sqlmethodattribute)。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義匯總](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 使用者定義函數](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 使用者定義類型](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 預存程式](/dotnet/framework/data/adonet/sql/clr-stored-procedures)   
 [CLR 觸發程序](/dotnet/framework/data/adonet/sql/clr-triggers)  
  
