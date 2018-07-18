---
title: 程式設計 AMO 互補的類別和方法 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: db41dcbcd16d6fe9ba6166f82f2939ef284bd4ba
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025085"
---
# <a name="programming-amo-complementary-classes-and-methods"></a>程式設計 AMO 互補的類別和方法
  本主題包含下列幾節：  
  
-   [組件類別](#Assembly)  
  
-   [備份與還原](#BU)  
  
-   [Trace 類別](#TRC)  
  
-   [CaptureLog 類別和 CaptureXML 屬性](#CL)  
  
##  <a name="Assembly"></a> 組件類別  
 組件可讓使用者擴充功能的[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]加入新的預存程序或多維度運算式 (MDX) 函數。 如需詳細資訊，請參閱[AMO 其他類別和方法](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)。  
  
 加入和卸除組件很簡單而且可以在線上執行。 您必須是資料庫管理員才能將組件加入資料庫，或者必須是伺服器管理員才能將組件加入伺服器物件。  
  
 下列範例會將組件加入提供的資料庫中，並指派服務帳戶以執行組件。 如果組件是在資料庫中，會先卸除組件，再嘗試加入它。  
  
```  
static public void CreateStoredProcedures(Database db)  
{  
    ClrAssembly clrAssembly;  
  
    // Verify That assembly exist in database and drop it  
    if (db.Assemblies.ContainsName("StoredProcedures"))  
    {  
        clrAssembly = db.Assemblies.FindByName("StoredProcedures");  
        clrAssembly.Drop();  
    }  
  
    // Create the CLR assembly  
    clrAssembly = db.Assemblies.Add("StoredProcedures");  
    clrAssembly.ImpersonationInfo = new ImpersonationInfo(  
        ImpersonationMode.ImpersonateServiceAccount);  
    clrAssembly.PermissionSet = PermissionSet.Unrestricted;  
  
    // Load the assembly files  
    clrAssembly.LoadFiles(Environment.CurrentDirectory  
        + @"\StoredProcedures2.dll", false);  
  
    clrAssembly.Update();  
}  
  
```  
  
##  <a name="BU"></a>Backup 與 Restore 方法  
 備份與還原方法可讓管理員備份資料庫並加以還原。  
  
 下列範例會為指定伺服器中的所有資料庫建立備份。 如果備份檔案已經存在，則會覆寫該檔案。 備份檔案會儲存在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Data 資料夾的 BackUp 資料夾中。  
  
```  
static public void BackUpAllDatabases(Server svr)  
{  
    string fileName;  
    if ((svr != null) && ( svr.Connected))  
        foreach (Database db in svr.Databases)  
        {  
            fileName = db.Name + "_" + ((Int64)(DateTime.Today.Year * 10000 + DateTime.Today.Month * 100 + DateTime.Today.Day)).ToString()+ ".abf";  
            db.Backup(fileName, true);  
        }  
}  
```  
  
 下列範例會從上一個範例還原 "Adventure Works" 備份。 如果 "My Adventure WorksDW" 資料庫已經存在，則會覆寫資料庫。  
  
```  
static public void RestoreAdventureWorks(Server svr)  
{  
    svr.Restore("Adventure Works DW_20051025.abf", "My Adventure WorksDW", true);  
}  
```  
  
##  <a name="TRC"></a> Trace 類別  
 監視伺服器活動需要使用兩種追蹤：工作階段追蹤與伺服器追蹤。 追蹤伺服器可以告訴您目前的工作在伺服器上執行的情形 (工作階段追蹤)，或者追蹤可以告訴您伺服器中的整體活動情形，甚至不必連接到伺服器 (伺服器追蹤)。  
  
 在追蹤目前的活動時 (工作階段追蹤)，伺服器會傳送通知給目前的應用程式，以說明伺服器中由應用程式造成的發生中事件。 事件是在目前的應用程式中使用事件處理常式來擷取。 您先將事件處理常式指派到 <xref:Microsoft.AnalysisServices.SessionTrace> 物件，然後啟動工作階段追蹤。  
  
 下列範例示範如何設定工作階段追蹤以追蹤目前的活動。 事件處理常式位於範例的結尾，而且會將所有的追蹤資訊都輸出到 System.Console 物件。 為了產生追蹤事件，將會在追蹤開始之後，完全處理 "Adventure Works" 範例 Cube。  
  
```  
static public void TestSessionTraces(Server svr)  
{  
    // Start the default trace  
  
    svr.SessionTrace.OnEvent  
        += new TraceEventHandler(DefaultTrace_OnEvent);  
    svr.SessionTrace.Stopped  
        += new TraceStoppedEventHandler(DefaultTrace_Stopped);  
    svr.SessionTrace.Start();  
  
    // Process the databases  
    // The trace handlers will output all progress notifications   
    // to the console  
    Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    cube.Process(ProcessType.ProcessFull);  
  
    // Stop the default trace  
    svr.SessionTrace.Stop();  
  
}  
static public void DefaultTrace_OnEvent(object sender, TraceEventArgs e)  
{  
    Console.WriteLine("{0}", e.TextData);  
}  
  
static public void DefaultTrace_Stopped(ITrace sender, TraceStoppedEventArgs e)  
{  
    switch (e.StopCause)  
    {  
        case TraceStopCause.StoppedByUser:  
        case TraceStopCause.Finished:  
            Console.WriteLine("Processing completed successfully");  
            break;  
  
        case TraceStopCause.StoppedByException:  
            Console.WriteLine("Processing failed: {0}",  
                e.Exception.Message);  
            break;  
    }  
}  
```  
  
 伺服器追蹤可以設定成將所有事項記錄到追蹤檔案，而且可以在服務重新啟動時，自動重新啟動。  
  
 若要設定伺服器追蹤，您需要先定義要監視的伺服器內事件，以及事件中的哪些資料應該儲存在追蹤檔案中。 對於每個事件，您必須定義要儲存在追蹤檔案中的資料行。  
  
 建立伺服器追蹤需要四個步驟：  
  
1.  建立伺服器追蹤物件並擴展基本的通用屬性。  
  
     LogFileSize 可定義追蹤檔案的大小上限，而且是以 MB 為單位；LogFileRollOver 允許記錄檔在 LogFileSize 到達上限時，換不同的檔案開始，並且會在啟用時以序號附加檔案名稱；如果服務重新啟動，AutoRestart 允許追蹤再次啟動。  
  
2.  建立事件和對應的資料行。  
  
3.  視需要啟動和停止追蹤。  
  
     即使已停止追蹤之後，追蹤仍然會在伺服器和如果追蹤定義為 AutoRestart 應該重新啟動 =**true**。  
  
4.  當不再需要時，就卸除追蹤。  
  
 在下列範例中，如果追蹤已經存在，會在卸除它後加以重建。 追蹤檔案會儲存在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Data 資料夾的 Log 資料夾中。  
  
```  
static public void TestServerTraces(Server svr)  
{  
    Trace trc;  
    TraceEvent te;  
  
        trc = svr.Traces.FindByName("TestServerTraces");  
        if (trc != null)  
            trc.Drop();  
        trc = svr.Traces.Add("TestServerTraces", "TestServerTraces");  
        trc.LogFileName = ("TestServerTraces_" +((Int64)(DateTime.Now.Year * 10000 + DateTime.Now.Month * 100 + DateTime.Now.Day)).ToString() + "_" +  
                ((Int64)(DateTime.Now.Hour * 10000 + DateTime.Now.Minute * 100 + DateTime.Now.Second)).ToString() + ".trc");  
        trc.LogFileSize = 100;  
        trc.LogFileRollover = true;  
        trc.AutoRestart = false;  
  
        #region Define Events to trace & data columns per event  
        te = trc.Events.Add(TraceEventClass.ProgressReportBegin);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.StartTime);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
        te.Columns.Add(TraceColumn.NTCanonicalUserName);  
  
        te = trc.Events.Add(TraceEventClass.ProgressReportCurrent);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.CurrentTime);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
  
        te = trc.Events.Add(TraceEventClass.ProgressReportEnd);  
        te.Columns.Add(TraceColumn.TextData);  
        te.Columns.Add(TraceColumn.StartTime);  
        te.Columns.Add(TraceColumn.CurrentTime);  
        te.Columns.Add(TraceColumn.EndTime);  
        te.Columns.Add(TraceColumn.Success);  
        te.Columns.Add(TraceColumn.Error);  
        te.Columns.Add(TraceColumn.ObjectName);  
        te.Columns.Add(TraceColumn.ObjectPath);  
        te.Columns.Add(TraceColumn.DatabaseName);  
        te.Columns.Add(TraceColumn.NTCanonicalUserName);  
        #endregion  
  
        trc.Update();  
        trc.Start();  
  
        #region Process the Adventure Works Cube  
        // The trace settings will output all progress notifications   
        // to the trace file  
        Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
        Cube cube = db.Cubes.FindByName("Adventure Works");  
        cube.Process(ProcessType.ProcessFull);  
        #endregion  
  
        trc.Stop();  
        trc.Drop();  
  
}  
```  
  
##  <a name="CL"></a> CaptureLog 與 CaptureXml 屬性  
 CaptureLog 屬性允許您從 AMO 作業建立 XMLA 批次檔。 CaptureLog 允許您使用指令碼將伺服器物件編寫成資料庫、Cube、維度、採礦結構等等。  
  
 建立 CaptureLog 需要下列步驟：  
  
1.  開始擷取 XMLA 記錄設定伺服器屬性 CaptureXml 至**true**。  
  
     這個選項會開始將所有的 AMO 作業儲存到字串集合，而不是將它們傳送到伺服器。  
  
2.  如往常般啟動 AMO 活動，但是請記往這不會傳送任何動作到伺服器。 活動可以是任何作業，例如處理、建立、刪除、更新或是在物件上的任何其他動作。  
  
3.  停止擷取 XMLA 記錄重設到 CaptureXml **false**。  
  
4.  藉由檢閱 CaptureLog 字串集合中的每個字串，或是使用 ConcatenateCaptureLog 方法產生完整的字串，來檢閱擷取的 XMLA。 ConcatenateCaptureLog 可讓您產生 XMLA 批次做為單一交易，並將平行處理選項加入批次。  
  
 下列範例傳回含批次命令的字串，以便在 [Adventure Works DW Multidimensional 2012] 資料庫上的所有維度與所有 Cube 上執行完整處理。  
  
```  
static public string TestCaptureLog(Server svr)  
{  
    String capturedXmla = "";  
    if ((svr != null) && (svr.Connected))  
    {  
        svr.CaptureXml = true;  
  
        #region Actions to be captured to an XMLA file  
        //No action is executed during CaptureXml = true  
        Database db = svr.Databases.FindByName("Adventure Works DW Multidimensional 2012");  
        foreach (Dimension dim in db.Dimensions)  
            dim.Process(ProcessType.ProcessFull);  
        foreach (Cube cube in db.Cubes)  
            cube.Process(ProcessType.ProcessFull);  
        #endregion  
  
        svr.CaptureXml = false;  
  
        capturedXmla = svr.ConcatenateCaptureLog(true, true);  
  
    }  
  
    return capturedXmla;  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices>   
 [AMO 類別簡介](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO 其他類別和方法](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)   
 [邏輯架構 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [資料庫物件 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [處理多維度模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
