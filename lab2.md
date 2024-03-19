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
/*x jest dzieckiem y*/

siblings(X,Y) :-
    parent(X,Z),
    parent(Y,Z).

cousins(X,Y) :-
    parent(X,Z),
    parent(Z,Q),
    parent(Y,W),
    parent(W,Q).

common_grandchild(X,Y) :-
    parent(Z,X),
    parent(Q,Y),
    parent(W,Q),
    parent(W,Z).
    
foster_child(X,Y) :-
    parent(X,Q),
    parent(Z,Q),
    parent(Z,Y).
