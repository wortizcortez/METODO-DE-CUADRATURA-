# METODO-DE-CUADRATURA-
%Método de la cuadratura

function [p N] = cuadra(fuc,A,B,TOL)

%valores de entrada:
%	fuc: Es una función para calcular su integral.
%	A y B: Son los extremos del intervalo  
%	TOL: Es la tolerancia que deseamos tener en la aproximación de la integral.

%Valores de salida:
%	la función devuelve un vector [p N]; donde p es la aproximación a la integral y N es 
%	la cantidad de veces que se evaluo la función para tener el valor p de la integral de fun.
%
APP = 0; %aproximacion para la integra

N = 3; %cuantas iteraciones debemos hacer para tener la tolerancia deseada.

i = 1;

TOL(i) = 10*TOL;

a(i) =  A;

h(i) = (B-A)/2;

FA(i) = feval(fuc,A);

FC(i) = feval(fuc,A + h(i));

FB(i) = feval(fuc,B);

S(i) = h(i)*(FA(i)+4*FC(i)+FB(i))/3;

L(i) = 1;

while i>0 
	FD = feval(fuc,a(i) + h(i)/2);
	FE = feval(fuc,a(i) + 3*h(i)/2);
	S1 = h(i)*(FA(i)+4*FD +FC(i))/6;
	
	S2 = h(i)*(FC(i)+4*FE +FB(i))/6;
	v1 = a(i);
	v2 = FA(i);
	v3 = FC(i);
	v4 = FB(i);
	v5 = h(i);
	v6 = TOL(i);
	v7 = S(i);
	v8 = L(i);
	
	i = i-1;
	if abs(S1+S2-v7)<v6
		APP = APP +(S1+S2);
	else
		%if(v8>=N)
		%	error ('nivel excedido')
		%	break
		i=i+1; %datos del subitervalo de la derecha
		a(i) = v1 + v5;
		FA(i) = v3;
		FC(i) = FE;
		FB(i) = v4;
		h(i) = v5/2;
		TOL(i) = v6/2;
		S(i) = S2;
		L(i) = v8+1;
		i = i+1; %datos pero por la izquierda del subintervalo
		a(i) = v1;
		FA(i) = v2;
		FC(i) = FD;
		FB(i) = v3;
		h(i) = h(i-1);
		TOL(i) = TOL(i-1);
		S(i) = S1;
		L(i) = L(i-1);
	end
	N = N+2;
end
p = APP; %aproximacion por la telorancia
