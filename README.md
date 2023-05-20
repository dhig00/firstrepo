# firstrepo
P1=input("enter p1=");
Q1=input("enter q1=");
P2=input("enter p2=");
Q2=input("enter q2=");
if (doIntersect(P1,Q1,P2,Q2))
    disp("yes")
    disp("the point of intersection is:-")
    disp(intersect(P1,Q1,P2,Q2))
else
    disp("no")
end
  
function a =onSegment(p,q,r)
    if ( (q(1) <= max(p(1), r(1))) && (q(1) >= min(p(1), r(1))) && (q(2) <= max(p(2), r(2))) && (q(2) >= min(p(2), r(2))))
        a=true;
    else
        a=false;
    end
end
function b= orient(p, q, r)
    % to find the orient of an ordered triplet (p,q,r)
    % function returns the following values:
    % 0 : Collinear points
    % 1 : Clockwise points
    % 2 : Counterclockwise      
    val = twoDcross(r-p,r-q);
    if (val > 0)
          
        % Clockwise orient
       b=1;
    elseif (val < 0)
          
        % Counterclockwise orient
        b=2;
    else
          
        %Collinear orient
      b=0;
    end
end
function c=doIntersect(p1,q1,p2,q2)
      
    % Find the 4 orients required for 
    or1 = orient(p1, q1, p2);
    or2 = orient(p1, q1, q2);
    or3 = orient(p2, q2, p1);
    or4 = orient(p2, q2, q1);
  
    % General case
    if ((or1 ~= or2) && (or3 ~= or4))
        c=true;
    
    % Special Cases  
    % p1 , q1 and p2 are collinear and p2 lies on segment p1q1
    elseif ((or1 == 0) && onSegment(p1, p2, q1))
        c=true;
    
    % p1 , q1 and q2 are collinear and q2 lies on segment p1q1
    elseif ((or2 == 0) && onSegment(p1, q2, q1))
        c=true;
    
    % p2 , q2 and p1 are collinear and p1 lies on segment p2q2
    elseif ((or3 == 0) && onSegment(p2, p1, q2))
        c=true;
   
    % p2 , q2 and q1 are collinear and q1 lies on segment p2q2
    elseif ((or4 == 0) && onSegment(p2, q1, q2))
        c=true;
    
    else
    %If none of the cases
        c=false;
    end   
end

function vec = twoDcross(a,b)
    vec(1) = a(1)*b(2) - a(2)*b(1);
end
