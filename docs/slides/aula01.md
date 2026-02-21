
# Aula 1 — OO como Engenharia de Sistemas
## Revisão estrutural de Orientação a Objetos

---

## Objetivo da Aula

Revisar OO sob perspectiva **estrutural e arquitetural**, não sintática.

Ao final você deve compreender:

- OO como modelagem de responsabilidades
- OO como controle de complexidade
- OO como proteção de invariantes
- OO como mecanismo de evolução de sistemas

---

## Premissa

Vocês já sabem:

- Classes
- Encapsulamento
- Herança
- Polimorfismo

Mas engenharia exige entender:

- Responsabilidade
- Invariantes
- Acoplamento
- Coesão
- Evolução estrutural

---

## Programa vs Sistema

**Programa**
- Resolve problema imediato
- Curta vida útil
- Estrutura mínima

**Sistema**
- Evolui continuamente
- Controla complexidade
- Mantém invariantes
- Precisa suportar mudança

Pergunta:
Nosso código inicial é programa ou sistema?

---

## Estudo de caso

```java
public class LegacyBattle {
    public static int fight(String a, String b) {
        Random r = new Random();
        int hpA = 100;
        int hpB = 100;
        while (hpA > 0 && hpB > 0) {
            hpB -= r.nextInt(20);
            hpA -= r.nextInt(20);
        }
        return hpA > hpB ? 1 : 2;
    }
}
```

