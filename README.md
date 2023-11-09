# HSCP_Leyan
 

# 加入了typemode
see 

Data_ProducerAnalyzer_submit.py L46-50


options.register('TYPE', 2,
    VarParsing.multiplicity.singleton,
    VarParsing.varType.int,
    "0:Tk only, 1:Tk+Muon, 2:Tk+TOF, 3:TOF onlypwd, 4:Q>1, 5:Q<1"
) 

Line 341

process.HSCParticleAnalyzer.TypeMode = 2


# 更改了 Analyzer.cc 按照mattermost的建议
Hi @Leyan Li  ! I have a branch of the HSCP framework on my side, and I did manage to get the TOF with @Caroline Collard advices (on data and on signal MC) : 
I added a bool for protection (calibrateTOF_) and if I recall correctly, you should not use the tofCalculator since we don't have the calibration done yet (maybe caroline can confirm). So I only access the TOF information by replacing this : https://github.com/tvami/SUSYBSMAnalysis-HSCP/blob/108dbafc3462e37e7d496720a0549e7d755df253/Analyzer/plugins/Analyzer.cc#L2383-L2386
With this :

         tof = &(*tofMap)[hscp.muonRef()];
         dttof = &(*tofDtMap)[hscp.muonRef()];
         csctof = &(*tofCscMap)[hscp.muonRef()];
And I removed this : https://github.com/tvami/SUSYBSMAnalysis-HSCP/blob/108dbafc3462e37e7d496720a0549e7d755df253/Analyzer/plugins/Analyzer.cc#L250
and this : https://github.com/tvami/SUSYBSMAnalysis-HSCP/blob/108dbafc3462e37e7d496720a0549e7d755df253/Analyzer/plugins/Analyzer.cc#L529

Tell me if that helps


# crab配置问题
我目前只改动过：

[https://github.com/ky230/HSCP_Leyan/blob/5fd3d89721cf4b99bc09c33f5127c8a25a878d21/submitCrabJobsData_leyan.py#L64C1-L64C34](https://github.com/ky230/HSCP_Leyan/blob/ddf50132d3c2eedf1fcab8376bb0b2baf3ef6091/submitCrabJobsData_leyan.py#L64C1-L64C34)

config.JobType.maxMemoryMB = 2500


https://github.com/ky230/HSCP_Leyan/blob/5fd3d89721cf4b99bc09c33f5127c8a25a878d21/submitCrabJobsData_leyan.py#L70

config.Data.unitsPerJob = 50




