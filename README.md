# Respostas do "E o oscar vai para..."

* Quantos Oscars Natalie Portman ganhou?

R: 1

Q:
```sql
select count(*) from indicados_ao_oscar where nome_do_indicado like "%Natalie Portman%" and vencedor = "true";
```

---

* Amy Adams já ganhou algum Oscar?

R: Não, nenhum.

Q:
```sql
 select nome_do_indicado, vencedor from indicados_ao_oscar where nome_do_indicado like "%Amy Adams%";
```

---

* A série de filmes Toy Story ganhou um Oscar em quais anos?
R: Já, o Toy Story 3 e 4 nos anos de 2011 e 2020

Q:
```sql
 select * from indicados_ao_oscar where nome_do_filme like "%toy story%" and vencedor = "true";
```

---

* A partir de que ano que a categoria "Actress" deixa de existir?

R: A partir de 1976 não há dados de Actress.

Q:
```sql
select ano_cerimonia, categoria from indicados_ao_oscar where categoria = "Actress" order by ano_cerimonia desc limit 1;
```

---

* Quem ganhou o primeiro Oscar para Melhor Atriz? Em que ano?

R: Janet Gaynor

Q:
```sql
 SELECT * FROM indicados_ao_oscar WHERE categoria= "ACTRESS" AND vencedor = "true" limit 1;
```

---

* Na campo "Vencedor", altere todos os valores com "true" para 1 e todos os valores "false" para 0.

R: Feito

Q:
```sql
UPDATE indicados_ao_oscar
SET vencedor = "1"
WHERE vencedor = "true";

UPDATE indicados_ao_oscar
SET vencedor = "0"
WHERE vencedor = "false";
```

---

* Em qual edição do Oscar "Crash" concorreu ao Oscar?

R: 78

Q:
```sql
select * from indicados_ao_oscar where nome_do_filme like "Crash";
```

---

* O filme Central do Brasil aparece no Oscar?

R: Aparece duas vezes mas não ganhou nenhuma.

Q:
```sql
select * from indicados_ao_oscar where nome_do_filme = "central station";
```

---

* Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser.

R: Bem pessoal e dificil de achar filmes assim, mas escolhi 3 de animação muito bons
que não ganharam o Academy Awards

Q:
```sql
INSERT INTO indicados_ao_oscar(ano_filmagem,ano_cerimonia,cerimonia,categoria,nome_do_indicado,nome_do_filme,vencedor) 
VALUES (2004,2005,97,'Melhor Filme de Animação','Stephen Hillenburg','Bob Esponja: O Filme','true');

INSERT INTO indicados_ao_oscar(ano_filmagem,ano_cerimonia,cerimonia,categoria,nome_do_indicado,nome_do_filme,vencedor) 
VALUES (1999,2000,97,'Melhor Filme de Animação','Brad Bird','O Gigante de Ferro','true');

INSERT INTO indicados_ao_oscar(ano_filmagem,ano_cerimonia,cerimonia,categoria,nome_do_indicado,nome_do_filme,vencedor) 
VALUES (2007,2008,97,'Melhor Filme de Animação','Stephen J. Anderson','A Família do Futuro','true');
```

---

* Denzel Washington já ganhou algum Oscar?

R: Sim, um em 'Glory' e o outro em 'Training Day'.

Q:
```sql
select * from indicados_ao_oscar where nome_do_indicado = "Denzel Washington" and vencedor = "true";
```

---

* Quais os filmes que ganharam o Oscar de Melhor Filme?

R: Vários, mas quero citar em especial os filmes 'Everything Everywhere All at Once' e 'Parasite'

Q:
```sql
select nome_do_indicado, ano_filmagem, nome_do_filme, vencedor from indicados_ao_oscar where categoria = "best picture" and vencedor = "true";
```

---

* Bonus: Quais os filmes que ganharam o Oscar de Melhor Filme e Melhor Diretor na mesma cerimonia?

R: Muitos

Q:
```sql
SELECT nome_do_filme, ano_cerimonia, vencedor
FROM indicados_ao_oscar
WHERE categoria IN ('Best Picture', 'Directing')
  AND vencedor = 'True'

GROUP BY nome_do_filme, ano_cerimonia
HAVING COUNT(DISTINCT categoria) = 1
order by ano_cerimonia desc;
```

---

* Bonus: Denzel Washington e Jamie Foxx já concorreram ao Oscar no mesmo ano?

R: Não

Q:
```sql
select nome_do_filme, nome_do_indicado, ano_cerimonia, vencedor
from indicados_ao_oscar 
where nome_do_indicado in ("Denzel Washington", "Jamie Foxx") 
group by nome_do_filme, nome_do_indicado, ano_cerimonia, vencedor
order by ano_cerimonia desc;
```
