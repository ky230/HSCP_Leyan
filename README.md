# HSCP_Leyan
加入了typemode 




# 更改了 Analyzer/plugins/Analyzer.cc 按照mattermost的建议
Hi @Leyan Li  ! I have a branch of the HSCP framework on my side, and I did manage to get the TOF with @Caroline Collard advices (on data and on signal MC) : 
I added a bool for protection (calibrateTOF_) and if I recall correctly, you should not use the tofCalculator since we don't have the calibration done yet (maybe caroline can confirm). So I only access the TOF information by replacing this : https://github.com/tvami/SUSYBSMAnalysis-HSCP/blob/108dbafc3462e37e7d496720a0549e7d755df253/Analyzer/plugins/Analyzer.cc#L2383-L2386
With this :

         tof = &(*tofMap)[hscp.muonRef()];
         dttof = &(*tofDtMap)[hscp.muonRef()];
         csctof = &(*tofCscMap)[hscp.muonRef()];
And I removed this : https://github.com/tvami/SUSYBSMAnalysis-HSCP/blob/108dbafc3462e37e7d496720a0549e7d755df253/Analyzer/plugins/Analyzer.cc#L250
and this : https://github.com/tvami/SUSYBSMAnalysis-HSCP/blob/108dbafc3462e37e7d496720a0549e7d755df253/Analyzer/plugins/Analyzer.cc#L529

Tell me if that helps
