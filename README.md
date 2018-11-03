# Tradutor fonético pt-BR

O **todutrar** transcreve arquivos de texto para uma representação semi-fiel do IPA (Alfabeto Fonético Internacional). Algumas opções de transcrição são da variante carioca do português brasileiro; outras, da fonologia da língua portuguesa.

* [Exemplo](#exemplo)
* [Como usar](#como-usar)
* [Regras de transformação](#regras-de-tranformação)
* [Deficiências](#deficiências)

# Exemplo

### Original

Considere o parágrafo inicial de Memórias Póstumas de Brás Cubas (Machado de Assis):

>Algum tempo hesitei se devia abrir estas memórias pelo princípio ou pelo fim, isto é, se poria em primeiro lugar o meu nascimento ou a minha morte. Suposto o uso vulgar seja começar pelo nascimento, duas considerações me levaram a adotar diferente método: a primeira é que eu não sou propriamente um autor defunto, mas um defunto autor, para quem a campa foi outro berço; a segunda é que o escrito ficaria assim mais galante e mais novo. Moisés, que também contou a sua morte, não a pôs no intróito, mas no cabo; diferença radical entre este livro e o Pentateuco.

### Transcrito

Veja a transcrição fonética do mesmo parágrafo:

>AWgŨ tẼpU eZitei sI devi@ abri"2 est@S mẼmóri@S pelU prĨcípiU OW pelU fĨ , istU é , sI pori@ ẼI prĨmeirU luga"2 U mEW naSĨmẼtU OW a mĨ"3@ mo"2"TI . SupostU U uZU vUWga"2 sej@ KÕmeSa"2 pelU naSĨmẼtU , du@S KÕsideraSõIS mI levarÃW a adota"2 "DiferẼ"TI métodU : a prĨmeir@ é KI EW nÃW sOW propriÃmẼ"TI Ũ AWto"2 defŨtU , m@S Ũ defŨtU AWto"2 , par@ KẼI a KÃp@ foi OWtrU be"2SU ; a segŨd@ é KI U esKritU fiKari@ aSĨ mais galÃ"TI I mais novU . MoiZés , KI tÃbẼI KÕtOW a su@ mo"2"TI , nÃW a pôs nU ĨtróitU , m@S nU KabU ; "DiferẼS@ "2a"DiKAW ẼtrI es"TI livrU I U PẼtatEWKU .

# Como usar

Clone ou baixe o repositório e execute o script *todutrar.py* com Python 3+, utilizando os seguintes argumentos:

    todutrar.py entrada saúda codificação-da-entrada codificação-da-saída

1. Entrada: arquivo de texto original
2. Saída*: arquivo com a transcrição fonética (padrão: "fonetizado.txt")
3. Codificação da entrada*: codificação do arquivo original (padrão: "utf8")
4. Codificação da saída*: codificação do arquivo alvo (padrão: "utf8")


(*) **Argumentos opcionais**


# Regras de transformação

Parte das regras para consoantes foram adaptadas do projeto [Metaphone for Brazilian Portuguese](https://sourceforge.net/p/metaphoneptbr/code/ci/master/tree/README#l56).

### Notação

A notação é, em grande parte, a mesma das expressões regulares:

	v 	--> vogais
	c 	--> consoantes
	[]	--> qualquer caracter dentro dos colchetes
	[^]	--> qualquer caracter exceto os que estão dentro dos colchetes
	^	--> início da palavra
	$	--> final da palavra
	?	--> 1 ou 0
	+	--> 1 ou mais

### Regras

As regras são aplicadas a todas as palavras, na ordem em que aparecem. Considera-se palavra o conjunto de caracteres entre espaços que não contenha números.

	Y 				--> I

	W[LRv] 			--> V
	W[c] 			--> "0

	[AÃÁ][N]$ 		--> Ã
	[AÃÁ][M]$ 		--> ÃW
	[Ã][O]$ 		--> ÃW
	[EÉẼ][MN]$ 		--> ẼI
	[IÍĨ][MN]$ 		--> Ĩ
	[OÓÕ][MN]$ 		--> ÕW
	[UÚŨ][MN]$ 		--> Ũ
	[AÃÁ][N]S$ 		--> ÃS
	[AÁÃ][M]S$ 		--> ÃWS
	[Ã][O]S$ 		--> ÃWS
	[EÉẼ][MN]S$ 	--> ẼIS
	[IĨÍ][MN]S$ 	--> ĨS
	[OÓÕ][MN]S$ 	--> ÕWS
	[UÚŨ][MN]S$ 	--> ŨS

	[^SWNR]S[v] 	--> Z

	[AÂÁ][MN][^vH] 	--> Ã
	[EÊÉ][MN][^vH] 	--> Ẽ
	[IÎÍ][MN][^vH] 	--> Ĩ
	[OÔÓ][MN][^vH] 	--> Õ
	[UÛÚ][MN][^vH] 	--> Ũ
	[AÂÁ][MN][v] 	--> Ã
	[EÊÉ][MN][v] 	--> Ẽ
	[IÎÍ][MN][v] 	--> Ĩ
	[OÔÒ][MN][v] 	--> Õ
	[UÛÚ][MN][v] 	--> Ũ
	[AÂÁ][MN][H] 	--> Ã
	[EÊÉ][MN][H] 	--> Ẽ
	[IÎÍ][MN][H] 	--> Ĩ
	[OÔÓ][MN][H] 	--> Õ
	[UÛÚ][MN][H] 	--> Ũ

	[AÁÂ][L][^vH] 	--> AW
	[EÉÊ][L][^vH] 	--> EW
	[IÍĨ][L][^vH]	--> IW
	[OÓÔ][L][^vH] 	--> OW
	[UŨÚ][L][^vH] 	--> UW
	[AÁÂ][L]$ 		--> AW
	[EÉÊ][L]$ 		--> EW
	[IĨÍ][L]$ 		--> IW
	[OÓÔ][L]$ 		--> OW
	[UŨÚ][L]$ 		--> UW
	[AÁÂ][U] 		--> AW
	[EÉÊ][U] 		--> EW
	[IÍĨ][U] 		--> IW
	[OÓÔ][U] 		--> OW
	[UÚŨ][U] 		--> UW

	[O]$ 			--> U
	[O][S]$ 		--> US
	[E]$ 			--> I
	[E][S]$ 		--> IS
	[A]$ 			--> @
	[A][S]$ 		--> @S
	[Z]$ 			--> S

	[T][IĨÍ] 		--> "T
	[D][IĨÍ] 		--> "D

	SS 				--> S
	SH 				--> X
	SC[EIẼĨÉÍ] 		--> S
	SC[AUOÃŨÕÁÚÓ] 	--> SK
	SCH 			--> X

	TH 				--> T
	^EX[v] 			--> Z
	EX[AOUÁÓÚÃÕŨ] 	--> KS
	EX[PTC] 		--> S
	EX[^EIAOUẼĨÃÕŨÉÍÁÓÚ] 			--> KS
	[DFMNPQSTVZ][AIOUÃĨÕŨÁÍÓÚ]X 	--> KS

	CHR 			--> K
	CH 				--> X
	C[ÂAÃÔÕOÛŨU] 	--> K
	C[c]			--> K
	C[EÊẼIÎĨ] 		--> S
	C$ 				--> K
	Ç 				--> S
	GH?[EẼÉIĨÍ] 	--> J
	^H[v] 			--> desaparece
	LH 				--> "1
	N$ 				--> M
	NH 				--> "3
	PH 				--> F

	QU[IEĨẼÍÉÎÊ] 	--> K
	QU[AOÃÕÁÓÂÔ] 	--> K
	Q 				--> K
	GU[IEĨẼÍÉÎÊ] 	--> G

	^R 				--> "2
	R$ 				--> "2
	RR 				--> "2
	R[c] 			--> "2

# Deficiências
* O **todutrar** não consegue identificar as sílabas tônicas das palavras e, por isso, algumas transcrições fonéticas não conseguem ser fiéis à fala do português brasileiro. Exemplo:
