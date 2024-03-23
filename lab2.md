# zadanie11

lubi(maciek,pawel).

lubi(pawel,krzysztof).

lubi(pawel,maciek).

lubi(jan,bartek).

lubi(bartek,jan).

przyjazn(X,Y) :-

    lubi(X,Y),
    
    lubi(Y,X).

niby_przyjazn(X,Y) :-

    lubi(X,Y);
    
    lubi(Y,X).

nieprzyjazn(X,Y) :-

    \+lubi(X,Y),
    
    \+lubi(Y,X).

love(X,Y) :-
    lubi(X,Y),
    
    lubi(Y,X),
    
    \+ (lubi(X,Z), Z\=Y),
    
    \+ (lubi(Y,Z), Z\=X).

# zadanie1
parent(syn,ojciec).

parent(syn,matka).

parent(corka,ojciec).

parent(corka,matka).

parent(matka,dziadek).

parent(matka,babcia).

parent(ojciec,dziadek2).

parent(ojciec,babcia2).

parent(ciotka,dziadek).

parent(ciotka,babcia).

parent(ciotka,dziadek2).

parent(ciotka,babcia2).

parent(kuzyn,ciotka).

parent(corka_p,ojciec).

parent(syn_p,matka).


/* x jest dzieckiem y */


siblings(X,Y) :-

    parent(X,Z).

    parent(Y,Z).


cousins(X,Y) :-

    parent(X,Z).

    parent(Z,Q).

    parent(Y,W).

    parent(W,Q).


common_grandchild(X,Y) :-

    parent(Z,X).

    parent(Q,Y).

    parent(W,Q).

    parent(W,Z).


foster_child(X,Y) :-

    parent(X,Q).

    parent(Z,Q).

    parent(Z,Y).

    \+ parent(X,Y).

    X \= Y.


step_siblings(X,Y) :-

    parent(X,Q).

    parent(X,Z).

    parent(Y,Z).

    parent(Y,W).

    \+ parent(X,Y).

    X \= Y.


sibling_in_law(X,Y) :-

    parent(Z,X).

    parent(Z,Q).

    parent(Q,W).

    parent(Y,W).


g(X,Y) :- 

    parent(X,Z).

    parent(X,W).

    parent(Y,W).

    parent(Y,Q).

    parent(Q,Z).

# zadanie2

rodzic(marek, anna).

rodzic(marek, jan).

rodzic(ewa, anna).

rodzic(ewa, jan).

rodzic(ewa, antek).

rodzic(marek, antek).

rodzic(halina, ewa).

rodzic(halina, jakub).

rodzic(andrzej, ewa).

rodzic(jakub, piotr).

rodzic(zygmunt, marek).

rodzic(stanislaw, zygmunt).


mężczyzna(marek).

mężczyzna(jan).

mężczyzna(antek).

mężczyzna(zygmunt).

mężczyzna(jakub).

mężczyzna(piotr).

mężczyzna(andrzej).

mężczyzna(stanislaw).


osoba(anna).

osoba(jan).

osoba(marek).

osoba(ewa).

osoba(zygmunt).

osoba(jakub).

osoba(piotr).

osoba(andrzej).

osoba(halina).


kobieta(X) :-

    \+ mężczyzna(X).


/*x jest ojcem y*/

ojciec(X, Y) :-

    mężczyzna(X),
    
    rodzic(X, Y).

matka(X, Y) :-

    kobieta(X),
    
    rodzic(X, Y).

corka(X, Y) :-

    kobieta(X),
    
    matka(X, Y);
    
    ojciec(X, Y).

brat_rodzony(X, Y) :-

    mężczyzna(X),
    
    ((ojciec(A, X), ojciec(A, Y));
    
    (matka(B, X), matka(B, Y))),
    
    X \= Y.

brat_przyrodni(X, Y) :-

    mężczyzna(X),
    
    rodzic(A, Y),
    
    rodzic(B, Y),
    
    (\+ rodzic(A, X);
    
    \+ rodzic(B, X)).
    
kuzyn(X, Y) :-

    rodzic(A, X),
    
    rodzic(B, A),
    
    rodzic(B, C),
    
    rodzic(C, Y),
    
dziadek_od_strony_ojca(X, Y) :-

    ojciec(X, A),
    
    ojciec(A, Y).

dziadek_od_strony_matki(X, Y) :-

    ojciec(X, A),
    
    matka(A, Y).

dziadek(X, Y) :-

    ojciec(X, A),
    
    rodzic(A, Y).

babcia(X, Y) :-
    matka(X, A),
    rodzic(A, Y).

wnuczka(X, Y) :-

    kobieta(Y),
    
    rodzic(A, Y),
    
    rodzic(X, A).

przodek_do2pokolenia_wstecz(X, Y) :-

    dziadek(X, Y);
    
    babcia(X, Y);
    
    rodzic(X,Y).

przodek_do3pokolenia_wstecz(X, Y) :-

    rodzic(X,Y);

    dziadek(X, Y);
    
    babcia(X, Y);
    
    (dziadek(Z, Y), rodzic(X, Z));
    
    (babcia(Z, Y), rodzic(X, Z)).








