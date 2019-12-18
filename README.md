# Pileup JetID

This branch contains the weights for pileup jetid for 2017 (94X) and 2018 (102X) data. These weights:

1. they are trained in eta bins [0, 2.5], [2.5, 2.75], [2.75, 3.0], [3.0, 5.0] different from previously shared recipe (2916 data).
2. Working points are still 81X, so the w.p. integrated or stored will not compatible with these trainings.
3. instead of using id flags use `mva` value to apply cut/id.


## Instructions to download weights

```
git clone -b 94X_weights_DYJets_inc_v2 git@github.com:cms-jet/PUjetID.git PUJetIDweights/
cp PUJetIDWeights/weights/pileupJetId_{94,102}X_Eta* $CMSSW_BASE/src/RecoJets/JetProducers/data/
git cms-merge-topic singh-ramanpreet:PUID_102_15_v2
rm -rf PUJetIDweights/  ### If needed
```

 ## Changes in config file
 
```
from RecoJets.JetProducers.PileupJetID_cfi import _chsalgos_94x, _chsalgos_102x
process.load(“RecoJets.JetProducers.PileupJetID_cfi”)
process.pileupJetId.jets = cms.InputTag(“ ... ”)
process.pileupJetId.inputIsCorrected = True
process.pileupJetId.applyJec = False
process.pileupJetId.vertexes = cms.InputTag(“offlineSlimmedPrimaryVertices”)
process.pileupJetId.algos = cms.VPSet(_chsalgos_)
```

## Scale Factors and uncertainties

In the folder ScaleFactors, root files containing the scale factors and uncertainties are included. 

   * [PUID_80XTraining_EffSFandUncties.root](ScaleFactors/PUID_80XTraining_EffSFandUncties.root): contains efficiencies, mistag rates, and uncertainties for 2016/2017/2018 samples using the 80X training.
