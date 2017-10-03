class: center, middle

#VCF File Demo
	
---
###Overview

* We will use a VCF file to demonstrate some of the practical uses of the Python that we've covered up to this point

--

* You can download the sample file using `curl`

```
curl https://raw.githubusercontent.com/andrewquitadamo/programming-fall2017/\
gh-pages/data/sample.vcf -O
```

--

* VCF files are used to represent genotypes

--

* We will remove any metadata line (they begin with ##)

--

* We will create an output file that contains the variant ID, and the parsed genotypes

--

* We will take the "0|0	1|0" and convert it to "0	1" etc.

---

###VCF Files

* VCF (Variant Call Format) files are a standard bioinformatics file format

--

```
#CHROM  POS ID  REF ALT QUAL    FILTER  INFO    FORMAT  HG00096	...
```

--

* The first three columns contain information about the genetic variant (position and ID)

--

* Columns 4 and 5 contain the reference and alternative allele

--

* Column 6 contains the quality information

--

* Column 7 contains filtering information

--

* Column 8 contains general information

--

* Column 9 indicates what the format of the genotypes are GT for genotype, DP for read depth, GL for genotype likelihood etc.

--

* The entire VCF specification is at http://samtools.github.io/hts-specs/VCFv4.1.print

---

###Open the file 

* Write some code to open up `sample.vcf` and loop through the lines one by one

--

* I would suggest using the `with open` syntax

--

```Python
with open('sample.vcf', 'r') as f:
    for line in f:
	   print(line)
```

---

###Dealing with metadata

* Add some code to skip the metadata lines (begin with ##), but not the header line (begins with a single #)

--

```Python
with open('sample.vcf', 'r') as f:
    for line in f:
        if line.startswith('##'):
            continue
        print(line)
```

---

###Dealing with the header

* Add some code to save the header to a variable

--

```Python
with open('sample.vcf', 'r') as f:
    for line in f:
        if line.startswith('##'):
            continue
        if line.startswith('#'):
            header = line
            continue
        print(line)
```

---

###Get the id and genotype fields

* Use the `.split()` method to convert each line to a list

--

```Python
with open('sample.vcf', 'r') as f:
    for line in f:
        if line.startswith('##'):
            continue
        if line.startswith('#'):
            header = line
            continue 
		fields = line.split()
		id = fields[2]
		genotypes = fields[9:]
```

---

###Update genotypes

* Add the genotype fields to get a single genotype

--

```Python
with open('sample.vcf', 'r') as f:
    for line in f:
        if line.startswith('##'):
            continue
        if line.startswith('#'):
            header = line
            continue 
        fields = line.split()
        id = fields[2]
        genotypes = fields[9:]
		for i, genotype in enumerate(genotypes):
            genos = genotype.split('|')
			genotype = int(genos[0]) + int(genos[1])
			genotypes[i] = genotype
```

---

###Create a new string with the genotypes

--
```Python
with open('sample.vcf', 'r') as f:
    for line in f:
        if line.startswith('##'):
            continue
        if line.startswith('#'):
            header = line
            continue
        fields = line.split()
        id = fields[2]
        genotypes = fields[9:]
        for i, genotype in enumerate(genotypes):
            genos = genotype.split('|')
            genotype = int(genos[0]) + int(genos[1])
            genotypes[i] = genotype 
			geno = id + "\t".join(map(str,genotypes))
		print(geno)
```

---

###Save results to a file

--

```Python
with open('sample.vcf', 'r') as f:
    with open('output.vcf', 'w') as fo:
        for line in f:
            if line.startswith('##'):
                continue
            if line.startswith('#'):
                header = line
                continue
            fields = line.split()
            id = fields[2]
            genotypes = fields[9:]
            for i, genotype in enumerate(genotypes):
                genos = genotype.split('|')
                genotype = int(genos[0]) + int(genos[1])
                genotypes[i] = genotype 
            geno = id + "\t".join(map(str,genotypes)) 
            print(geno, file=fo)
```

---

###Add the header to the file

--

```Python
with open('sample.vcf', 'r') as f:
    with open('output.vcf', 'w') as fo:
        for line in f:
            if line.startswith('##'):
                continue
            if line.startswith('#'):
				fields = line.split()
			    print(fields[2], "\t".join(fields[9:]), sep='\t', file=fo)
			 	continue
            fields = line.split()
            id = fields[2]
            genotypes = fields[9:]
            for i, genotype in enumerate(genotypes):
                genos = genotype.split('|')
                genotype = int(genos[0]) + int(genos[1])
                genotypes[i] = genotype
            geno = id + "\t".join(map(str,genotypes))    
            print(geno, file=fo)
```

---

###Reading to a dictionary

```Python
svs = {}
with open('sample.vcf', 'r') as f:
    with open('output.vcf', 'w') as fo:
        for line in f:
            if line.startswith('#'):
                continue 
            fields = line.split()
            id = fields[2]
            genotypes = fields[9:]
            for i, genotype in enumerate(genotypes):
                genos = genotype.split('|')
                genotype = int(genos[0]) + int(genos[1])
                genotypes[i] = genotype
            genotypes = "\t".join(map(str,genotypes))
            svs[id] = genotypes
```

--

```Python
svs['DUP_delly_DUP20532']
```
