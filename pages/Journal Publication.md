- The list of species that have less than 10 chromosomes and actually have assemblies according to NCBI entrez
  collapsed:: true
	- Numbers for assemblies generated using this one-liner :`esearch -db assembly -query $line | xtract -pattern ENTREZ_DIRECT -element Count`
	- The name of the bash script used is `entrez_automation` and the jupyter notebook used was `6.ipynb`
	- Dysphania ambrosioides
	  Aristolochia cretica
	  Arabidopsis thaliana
	  Brassica napus
	  Brassica rapa
	  Erucastrum elatum
	  Physaria acutifolia
	  Physaria berlandieri
	  Physaria cinerea
	  Physaria cordiformis
	  Physaria geyeri
	  Physaria lepidota
	  Physaria oregona
	  Physaria palmeri
	  Physaria parvula
	  Physaria rectipes
	  Physaria reediana
	  Physaria rollinsii
	  Physaria valida
	  Physaria vitulifera
	  Bradburia pilosa
	  Emilia baberka
	  Erigeron arizonicus
	  Erigeron philadelphicus
	  Erigeron vetensis
	  Osbertia stolonifera
	  Pulicaria angustifolia
	  Senecio lelyi
	  Senecio nikoensis
	  Sedum pusillum
	  Cucurbita pepo
	  Rhynchospora breviuscula
	  Rhynchospora tenuis
	  Ricinus communis
	  Juncus effusus
	  Juncus sorrentinii
	  Cicer echinospermum
	  Cicer reticulatum
	  Lupinus barkeri
	  Sesbania bispinosa
	  Vicia faba
	  Vicia sativa
	  Vicia serinica
	  Vicia sosnowskyi
	  Theobroma cacao
	  Corrigiola litoralis
	  Erycina pusilla
	  Oxalis juruensis
	  Oxalis praetexta
	  Macleaya cordata
	  Plantago insularis
	  Plantago major
	  Brachypodium distachyon
	  Coix aquatica
	  Coix lacryma-jobi
	  Digitaria aequiglumis
	  Oropetium thomaeum
	  Pennisetum glaucum
	  Morinda officinalis
	  Santalum album
	  Tetracentron sinense
	  Pleurozium schreberi
	  Rhytidiadelphus loreus
- It seems very possible that `NCBI entrez` might not be the way to go and the only way to do this might be with [`NCBI datasets`](https://www.ncbi.nlm.nih.gov/datasets/docs/v2/how-tos/)
  collapsed:: true
	- The issue with NCBI has been that for some reason it is completely ignoring the specific name of a whole species name (using `datasets summary genome taxon 'Aristolochia cretica'`). For example, when sending in `datasets summary genome taxon 'Aristolochia cretica'`, only `Aristolochia` is used.
- `esearch -db assembly -query "Aristolochia cretica" | efetch -format uid` this is it.
	- `efetch -db assembly -id 10829611` produces an error that just says "Bad request"
	- `efetch -db assembly -id 10829611 -format xml` does not work either.
- This is it: `esearch -db assembly -query "Aristolochia cretica" | esummary`
- This produces the proper species names: `esearch -db assembly -query "Aristolochia cretica" | esummary | xtract -pattern DocumentSummary -element SpeciesName`
- I completely forget why I dropped the following species:
	- Lonchitis hirsuta - VVRN
	- Lindsaea microphylla - YIXP
	- Dennstaedtia davallioides - This one is MTGC and was particularly problematic because it was missing nucleotide data all together
- The list of species with 112 names is
  collapsed:: true
	- Acacia argyrophylla
	  Adiantum raddianum
	  Agave tequilana
	  Amborella trichopoda
	  Anemia tomentosa
	  Arabidopsis thaliana
	  Araucaria rulei
	  Aristolochia elegans
	  Asparagus densiflorus
	  Asplenium platyneuron
	  Atriplex prostrata
	  Austrobaileya scandens
	  Austrotaxus spicata
	  Azolla Pinnata
	  Azolla carliniana
	  Botrypus virginianus
	  Cedrus libani
	  Ceratophyllum demersum
	  Ceratopteris thalictroides
	  Chamaecyparis lawsoniana
	  Cleome gynandra
	  Cycas micholitzii
	  Cystopteris utahensis
	  Danaea nodosa
	  Dendrolycopodium obscurum
	  Dennstaedtia davallioides 
	  Dichroa febrifuga
	  Dioon edule
	  Diphasiastrum digitatum
	  Dipteris conjugata
	  Drimys winteri
	  Dryas octopetala
	  Eleusine coracana
	  Ephedra sinica
	  Equisetum diffusum
	  Equisetum hyemale
	  Erigeron canadensis
	  Eschscholzia californica
	  Freycinetia multiflora
	  Gaga arizonica
	  Ginkgo biloba
	  Gnetum montanum
	  Gymnocarpium dryopteris
	  Hakea drupacea
	  Heliotropium mendocinum
	  Huperzia lucidula
	  Huperzia myrsinites
	  Huperzia squarrosa
	  Hydrocotyle umbellata
	  Hymenophyllum bivalve
	  Isoetes tegetiformans
	  Leiosporoceros dussii
	  Lindenbergia philippensis
	  Lindsaea linearis
	  Lindsaea microphylla
	  Lonchitis hirsuta
	  Loropetalum chinense
	  Lycopodiella appressa
	  Lycopodium annotinum
	  Lycopodium deuterodensum
	  Lygodium japonicum
	  Magnolia grandiflora
	  Marattia attenuata
	  Marchantia polymorpha
	  Marsilea quadrifolia
	  Metasequoia glyptostroboides
	  Metzgeria crassipilis
	  Nothoceros vincentianus
	  Nothotsuga longibracteata
	  Nuphar advena
	  Onoclea sensibilis
	  Ophioglossum petiolatum
	  Oryza sativa
	  Osmunda javanica
	  Osmundastrum cinnamomeum
	  Physcomitrella patens
	  Picea engelmannii
	  Pilularia globulifera
	  Pinus radiata
	  Plagiogyria japonica
	  Polypodium glycyrrhiza
	  Polystichum acrostichoides
	  Populus trichocarpa
	  Pseudolarix amabilis
	  Pseudolycopodiella caroliniana
	  Psilotum nudum
	  Pteris ensiformis
	  Pteris vittata
	  Rhododendron scopulorum
	  Salvinia natans
	  Santalum acuminatum
	  Sassafras albidum
	  Sceptridium dissectum
	  Selaginella apoda
	  Selaginella kraussiana
	  Selaginella moellendorffii
	  Selaginella selaginoides
	  Selaginella wallacei
	  Selaginella willdenowii
	  Sisyrinchium angustifolium
	  Solanum xanthocarpum
	  Sphagnum palustre
	  Taiwania cryptomerioides
	  Taxodium distichum
	  Thyrsopteris elegans
	  Timmia austriaca
	  Tmesipteris parva
	  Torreya taxifolia
	  Vittaria appalachiana
	  Wollemia nobilis
	  Zea may
	  Zingiber officinale
- The one with 110 names is
  collapsed:: true
	- Acacia argyrophylla 
	  Adiantum raddianum 
	  Agave tequilana 
	  Amborella trichopoda 
	  Anemia tomentosa 
	  Arabidopsis thaliana 
	  Araucaria rulei 
	  Aristolochia elegans 
	  Asparagus densiflorus 
	  Asplenium platyneuron 
	  Atriplex prostrata 
	  Austrobaileya scandens 
	  Austrotaxus spicata 
	  Azolla carliniana 
	  Azolla Pinnata 
	  Botrypus virginianus 
	  Cedrus libani 
	  Ceratophyllum demersum 
	  Ceratopteris thalictroides 
	  Chamaecyparis lawsoniana 
	  Cleome gynandra 
	  Cycas micholitzii 
	  Cystopteris utahensis 
	  Danaea nodosa 
	  Dendrolycopodium obscurum 
	  Dennstaedtia davallioides 
	  Dichroa febrifuga 
	  Dioon edule 
	  Diphasiastrum digitatum 
	  Dipteris conjugata 
	  Drimys winteri 
	  Dryas octopetala 
	  Eleusine coracana 
	  Ephedra sinica 
	  Equisetum diffusum 
	  Equisetum hyemale 
	  Erigeron canadensis 
	  Eschscholzia californica 
	  Freycinetia multiflora 
	  Gaga arizonica 
	  Ginkgo biloba 
	  Gnetum montanum 
	  Gymnocarpium dryopteris 
	  Hakea drupacea 
	  Heliotropium mendocinum 
	  Huperzia lucidula 
	  Huperzia myrsinites 
	  Huperzia squarrosa 
	  Hydrocotyle umbellata 
	  Hymenophyllum bivalve 
	  Isoetes tegetiformans 
	  Leiosporoceros dussii 
	  Lindenbergia philippensis 
	  Lindsaea linearis 
	  Loropetalum chinense 
	  Lycopodiella appressa 
	  Lycopodium annotinum 
	  Lycopodium deuterodensum 
	  Lygodium japonicum 
	  Magnolia grandiflora 
	  Marattia attenuata 
	  Marchantia polymorpha 
	  Marsilea quadrifolia 
	  Metasequoia glyptostroboides 
	  Metzgeria crassipilis 
	  Nothoceros vincentianus 
	  Nothotsuga longibracteata 
	  Nuphar advena 
	  Onoclea sensibilis 
	  Ophioglossum petiolatum 
	  Oryza sativa 
	  Osmunda javanica 
	  Osmundastrum cinnamomeum 
	  Physcomitrella patens 
	  Picea engelmannii 
	  Pilularia globulifera 
	  Pinus radiata 
	  Plagiogyria japonica 
	  Polypodium glycyrrhiza 
	  Polystichum acrostichoides 
	  Populus trichocarpa 
	  Pseudolarix amabilis 
	  Pseudolycopodiella caroliniana 
	  Psilotum nudum 
	  Pteris ensiformis 
	  Pteris vittata 
	  Rhododendron scopulorum 
	  Salvinia natans 
	  Santalum acuminatum 
	  Sassafras albidum 
	  Sceptridium dissectum 
	  Selaginella apoda 
	  Selaginella kraussiana 
	  Selaginella moellendorffii 
	  Selaginella selaginoides 
	  Selaginella wallacei 
	  Selaginella willdenowii 
	  Sisyrinchium angustifolium 
	  Solanum xanthocarpum 
	  Sphagnum palustre 
	  Taiwania cryptomerioides 
	  Taxodium distichum 
	  Thyrsopteris elegans 
	  Timmia austriaca 
	  Tmesipteris parva 
	  Torreya taxifolia 
	  Vittaria appalachiana 
	  Wollemia nobilis 
	  Zea may 
	  Zingiber officinale
- # [[Feb 14th, 2023]]
- I used `8.ipynb` to compare the old list of 110 species and the new list of species with 35 (34 + Arabidopsis thaliana). The only similarity was Arabidopsis which I dropped from the list with 35 names.
  collapsed:: true
	- The list of 34 species is as follows:
	  collapsed:: true
		- Dysphania ambrosioides
		  Brassica napus
		  Brassica rapa
		  Erucastrum elatum
		  Physaria acutifolia
		  Erigeron philadelphicus
		  Cucurbita pepo
		  Rhynchospora breviuscula
		  Rhynchospora pubera
		  Rhynchospora tenuis
		  Ricinus communis
		  Juncus effusus
		  Cicer echinospermum
		  Cicer reticulatum
		  Sesbania bispinosa
		  Vicia faba
		  Vicia sativa
		  Theobroma cacao
		  Corrigiola litoralis
		  Erycina pusilla
		  Macleaya cordata
		  Turnera subulata
		  Plantago major
		  Plantago ovata
		  Brachypodium distachyon
		  Coix aquatica
		  Coix lacryma-jobi
		  Oropetium thomaeum
		  Pennisetum glaucum
		  Morinda officinalis
		  Santalum album
		  Tetracentron sinense
		  Pleurozium schreberi
		  Rhytidiadelphus loreus
- `esearch -db assembly -query "Brassica rapa[ORGN]" | esummary | xtract -pattern DocumentSummary -sep "|" -element GbUid SpeciesName AssemblyStatus AssemblyType LastUpdateDate`
- # [[Feb 15th, 2023]]
- What is the different between a scaffold level assembly and a chromosome level assembly
  :LOGBOOK:
  CLOCK: [2023-02-15 Wed 12:57:25]--[2023-02-15 Wed 12:57:26] =>  00:00:01
  CLOCK: [2023-02-15 Wed 12:57:27]--[2023-02-15 Wed 12:57:27] =>  00:00:00
  :END:
	- According to [ensemble](https://useast.ensembl.org/info/genome/genebuild/chromosomes_scaffolds_contigs.html) and [JGI](https://mycocosm.jgi.doe.gov/help/scaffolds.jsf)
	- Contigs - continuous portion of a genome sequence reconstructed from shotgun data.
	- Scaffolds - Are structures made of contigs and gaps.
	- Chromosomes - Chromosomes are scaffolds without gaps
- # [[Feb 23rd, 2023]]
- Comments from Norm
	- *When using transcriptomes there can be a lot of assembly error, and the data may include alternative splice forms. Even though the 1KP data is relatively cleaned up for these issues, there are likely (well, not likely, I happen to know for a fact) still more than a single sequence that represents a gene. The effect of this is that you may be over-counting membership in a gene family, particularly when you have mixed genome/transcriptome data. If it’s not too late, I would look into tree-based methods of selecting the single best transcript for any one gene - we’ve used this in the path and I quite like it: https://bitbucket.org/dfmoralesb/target_enrichment_orthology/src/master/ (there is another implementation I haven’t tried that may be easier to use here: https://github.com/chrisjackson-pellicle/Yang-and-Smith-paralogy-resolution).*
	- *This is a bit more of a “philosophical” issue, but I think it would be good to think about how to really associate gene family changes or selection with the evolution of heterospory. I guess what I’m getting at is that you (or we) should think about what other traits may have arisen at the same nodes where heterospory arises. How can we be sure that we’re not looking at an association with other traits? The best way to do this would be to include other clades where those traits have evolved in homosporous lineages, or in heterosporous lineages but much later than the evolution of heterospory. I’m not sure how much of a big deal this is, but it’s just a little nagging thought in the back of my head*
- Thesis Feedback from Norm (not in order)
  collapsed:: true
	- *However, the scientific community still lacks a plausible explanation for this association of two seemingly unrelated traits.*
		- Norm said: *They could still be unrelated! To test this, it would be interesting to look at other nodes where chromosome numbers have decreased. If the same genes are involved at these nodes as your 3 focal nodes, you could potentially eliminate some of the candidates!*
		-
- # [[Feb 28th, 2023]]
- {{embed [[Working with SoapDenovo-Trans]]}}
- # [[Mar 2nd, 2023]]
- Tasks
	- Make a list of the old 111 species
	  collapsed:: true
		- Do this using the peptide files in onedrive
	- Split the list according to sources
		- Down the onekp data using the Rpackage.
		- If you are going to use Jessie's data do it using his github.
		- Use phytozome for Blaine's species
			- {{embed ((6400e71b-3b0c-46a5-8ac7-644228ebc376))}}
			- |Species X Source|Blaine|Phytozome primary transcript|Phytozome transcript|
			  |--|--|--|--|
			  |Arabidopsis thaliana|27628|27654|48455|
			  |Oryza sativa|42189|42189|52424|
			  |Physcomitrella paten |32926|32926|87533|
			  |Poplus trichocarpa|34699|42950|63498|
			  |Zea mays|39756|39498|131484|
			-
	- TODO Not sure why but there are two different types of genome files on phytozome, for both peptides and cds files. One type that is labelled `.cds_primaryTranscriptOnly.fa.gz` and the second type is labelled `cds.fa.gz`. Not sure what the difference is.
	  collapsed:: true
	  :LOGBOOK:
	  CLOCK: [2023-03-02 Thu 14:10:55]--[2023-03-02 Thu 14:10:56] =>  00:00:01
	  :END:
		- [Discussion on reddit](https://www.reddit.com/r/bioinformatics/comments/11gd520/transcript_vs_primary_transcript_on_phytozome/)
		- [Discussion on biostars](https://www.biostars.org/p/9556284/)
		- [According to Wikidpedia](https://www.wikiwand.com/en/Primary_transcript) A primary transcript is the single-stranded ribonucleic acid (RNA) product synthesized by transcription of DNA, and processed to yield various mature RNA products such as mRNAs, tRNAs, and rRNAs. The primary transcripts designated to be mRNAs are modified in preparation for translation. For example, a precursor mRNA (pre-mRNA) is a type of primary transcript that becomes a messenger RNA (mRNA) after processing.
	-
- # [[Mar 10th, 2023]]
- Removed MTGC (Dennstaedtia davallioides) from the list because it has no assembly on onekp archives. But there is data on Jessie's repo.
- So the Onekp list of species is really 101 species long because of the removal of MTGC (which we might get from Jessie)
- So the onekp list is
  collapsed:: true
	- Acacia argyrophylla
	  Adiantum raddianum
	  Agave tequilana
	  Amborella trichopoda
	  Anemia tomentosa
	  Araucaria rulei
	  Aristolochia elegans
	  Asparagus densiflorus
	  Asplenium platyneuron
	  Atriplex prostrata
	  Austrobaileya scandens
	  Austrotaxus spicata
	  Botrypus virginianus
	  Cedrus libani
	  Ceratophyllum demersum
	  Ceratopteris thalictroides
	  Chamaecyparis lawsoniana
	  Cleome gynandra
	  Cycas micholitzii
	  Cystopteris utahensis
	  Danaea nodosa
	  Dendrolycopodium obscurum
	  Dichroa febrifuga
	  Dioon edule
	  Diphasiastrum digitatum
	  Dipteris conjugata
	  Drimys winteri
	  Dryas octopetala
	  Eleusine coracana
	  Ephedra sinica
	  Equisetum diffusum
	  Equisetum hyemale
	  Erigeron canadensis
	  Eschscholzia californica
	  Freycinetia multiflora
	  Gaga arizonica
	  Ginkgo biloba
	  Gnetum montanum
	  Gymnocarpium dryopteris
	  Hakea drupacea
	  Heliotropium mendocinum
	  Huperzia lucidula
	  Huperzia myrsinites
	  Huperzia squarrosa
	  Hydrocotyle umbellata
	  Hymenophyllum bivalve
	  Isoetes tegetiformans
	  Leiosporoceros dussii
	  Lindenbergia philippensis
	  Lindsaea linearis
	  Lindsaea microphylla
	  Lonchitis hirsuta
	  Loropetalum chinense
	  Lycopodiella appressa
	  Lycopodium annotinum
	  Lycopodium deuterodensum
	  Lygodium japonicum
	  Magnolia grandiflora
	  Marattia attenuata
	  Marchantia polymorpha
	  Metasequoia glyptostroboides
	  Metzgeria crassipilis
	  Nothoceros vincentianus
	  Nothotsuga longibracteata
	  Nuphar advena
	  Onoclea sensibilis
	  Ophioglossum petiolatum
	  Osmunda javanica
	  Osmundastrum cinnamomeum
	  Picea engelmannii
	  Pinus radiata
	  Plagiogyria japonica
	  Polypodium glycyrrhiza
	  Polystichum acrostichoides
	  Pseudolarix amabilis
	  Pseudolycopodiella caroliniana
	  Psilotum nudum
	  Pteris ensiformis
	  Pteris vittata
	  Rhododendron scopulorum
	  Santalum acuminatum
	  Sassafras albidum
	  Sceptridium dissectum
	  Selaginella apoda
	  Selaginella kraussiana
	  Selaginella moellendorffii
	  Selaginella selaginoides
	  Selaginella wallacei
	  Selaginella willdenowii
	  Sisyrinchium angustifolium
	  Solanum xanthocarpum
	  Sphagnum palustre
	  Taiwania cryptomerioides
	  Taxodium distichum
	  Thyrsopteris elegans
	  Timmia austriaca
	  Tmesipteris parva
	  Torreya taxifolia
	  Vittaria appalachiana
	  Wollemia nobilis
	  Zingiber officinale
- The onekp file stats
	- |Data|Total counts|SHA256|
	  |--|--|--|
	  |Peptide|1785616|24c8e47ae5315dfe1c1c4332a3d16c09409062d36f12a846dba9b7531ccb6dc7|
	  |Nucleotide|1785697|7f5f5719ca54c0141a94281be1ac4c26b9f528c37ec72bcf10a81ca060cb8ef0|
- The following species will be obtained from phytozome
  collapsed:: true
	- Arabidopsis thaliana
	- Oryza sativa
	- Physcomitrella paten
	- Poplus trichocarpa
	- Zea mays
	- Download all using this [curl one-liner](curl --cookie jgi_session=/api/sessions/fa5f76893896db3f28585eaa95f5932f --output download.20230310.171150.zip -d "{\"ids\":{\"Phytozome-447\":[\"587b0adb7ded5e4229d885a1\",\"587b0ade7ded5e4229d885aa\"],\"Phytozome-493\":[\"5c83121646d1e64ae3ba2bed\",\"5c83121646d1e64ae3ba2bec\"],\"Phytozome-318\":[\"56901c820d878508e3d1fc3c\",\"56901c820d878508e3d1fc3d\"],\"Phytozome-323\":[\"5693356b0d87851ee9726afb\",\"5693356b0d87851ee9726afe\"],\"Phytozome-444\":[\"587b0ae57ded5e4229d885be\",\"587b0ae77ded5e4229d885c4\"]}}" -H "Content-Type: application/json" https://files.jgi.doe.gov/filedownload/), which might not be future-proof (i.e. phytozome might re-organize their backend database.)
	  collapsed:: true
		- |Species|Nucleotide Counts|Peptide counts|
		  |--|--|--|
		  |Arabidopsis_thaliana|27654|27654|
		  |Oryza_sativa|42189|42189|
		  |Physcomitrella_patens|32926|32926|
		  |Poplus_trichocarpa|42950|42950|
		  |Zea_mays|39498|39498|
		  |Total|185217|185217|
	- |Archive name|Counts|Hash|
	  |--|--|--|
	  |Phytozome_cds.zip|185217|f229158e64852c8f540209be082da81777919137e60ba9614b77f37ed19de8b5|
	  |Phytozome_pep.zip|185217|aa49aa0728e4c0c2104e03068d56eda3098add856d81f73a1954cd5e2f167624|
- The following species will be obtained from [DOI]( https://doi.org/10.3389/fpls.2022.882441) and more specifically this data [repo](https://github.com/jessiepelosi/ferntxms)
	- Azolla caroliniana:
	- Azolla pinnata
	- Marsilea quadrifolia
	- Pilularia globulifera
	- Salvinia natans
	- Dennstaedtia davallioides
	- |Species|Pep counts|Nucleotide counts|
	  |--|--|--|
	  |Azolla cf. Caroliniana|32516|32516|
	  |Azolla pinnata|32453|32453|
	  |Dennstedtia davallioides|18761|18761|
	  |Marsilea quadrifolia|25002|25002|
	  |Pilularia globulifera|24353|24353|
	  |Salvinia natans|31068|31608|
	- |Archive|Hash|
	  |--|--|
	  |txms_cds.zip|2583352d826b68bfaba9d23ff281b2b0daa05681bee1aa75e0f4d1558607aae1|
	  |txms_peps.zip|742b64c07a434e1281642d902e23839fddb25675a4736d850d2552b51f2c0669|
- ## Task for header comparison
- I have two sets of files: peptide fasta files and nucleotide fasta files. The fasta files have "header" every other line -headers are defined by the `>` at the beginning of the line. For each *x* peptide fasta file there is a *x* nucleotide fasta file. A peptide header is the name for a peptide sequence and a nucleotide header is the name for a nucleotide header. For my use cases every peptide header must have its analogous nucleotide header and peptides headers without corresponding nucleotide headers need to be removed. I want to do this in python. what is the fastest data structure to use if each file can have tens of thousands of headers?
	-
- # [[Mar 15th, 2023]]
- The cleaned list of sequences is called `Final_Sequences.zip` and the SHA256 hash is 61a5e8190a989d92eb15845190e1cbb453725e28d225953211f7a9952da4e6bc .
- # [[Mar 17th, 2023]]
- For whatever reason `scaffold-ZCDJ-2084138-Acacia_argyrophylla-Nov.` is duplicated with dissimilar sequences.