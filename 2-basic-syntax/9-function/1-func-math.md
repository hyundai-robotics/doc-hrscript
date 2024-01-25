# 2.9.1 수학 함수

<table style="text-align:left">
	<thead>
		<tr>
			<th>함수</th>
			<th>설명</th>
			<th>사용 예</th>
			<th>결과</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>abs(a)</td>
			<td>a의 절대값 (absolute) 을 리턴합니다.</td>
			<td>abs(-300)</td>
				<td>300</td>
		</tr>
		<tr>
			<td>acos(a)</td>
			<td>a의 arc cosine값을 radian 형식으로 리턴합니다.</td>
			<td>acos(0.5)</td>
			<td>1.0472</td>
		</tr>
		<tr>
			<td>asin(a)</td>
			<td>a의 arc sige 값을 radian 형식으로 리턴합니다.</td>
			<td>asin(0.5)</td>
			<td>0.5236</td>
		</tr>
		<tr>
			<td>atan(a)</td>
			<td>a의 arctangent 값을 radian 형식으로 리턴합니다.</td>
			<td>atan(0.5)</td>
			<td>0.4636</td>
		</tr>
		<tr>
			<td>atan2(a, b)</td>
			<td>y길이가 a, x길이가 b인 삼각형의 arctangent 값을 radian 형식으로 리턴합니다.</td>
			<td>atan2(2,1)</td>
				<td>1.1071</td>
		</tr>
		<tr>
			<td>ceil(x)</td>
			<td>x의 올림 값을 리턴합니다.</td>
			<td>
				ceil(3.1415)<br>
				ceil(-3.1415)
			</td>
				<td>
				4<br>
				-3
				</td>
		</tr>
		<tr>
			<td>cos(r)</td>
			<td>radian 형식의 a의 cosine 값을 리턴합니다.</td>
			<td>cos(3.1415)</td>
			<td>-1</td>
		</tr>
		<tr>
			<td>deg2rad(d)</td>
			<td>degree 형식의 d의 radian 값을 리턴합니다.</td>
			<td>deg2rad(-90)</td>
			<td>-1.570796</td>
		</tr>
		<tr>
			<td>dist(x, y)</td>
			<td>원점에서 (x, y) 좌표까지의 유클리드 거리를 리턴합니다.</td>
			<td>dist(3.5,10)</td>
			<td>10.59481</td>
		</tr>
		<tr>
			<td>floor(x)</td>
			<td>x의 내림 값을 리턴합니다.</td>
			<td>
				floor(3.1415)<br>
				floor(-3.1415)
			</td>
			<td>
				3<br>
				-4
			</td>
		</tr>
		<tr>
			<td>max(a, b)</td>
			<td>a와 b중 큰 값을 리턴합니다.</td>
			<td>max(-1.23, -3)</td>
			<td>-1.23</td>
		</tr>
		<tr>
			<td>min(a, b)</td>
			<td>a와 b중 작은 값을 리턴합니다.</td>
			<td>max(-1.23, -3)</td>
			<td>-3</td>
		</tr>
		<tr>
			<td>near(a, b[,e])</td>
			<td>실수값 a와 b의 차이가 e보다 작거나 같으면 1, 크면 0을 리턴합니다.</td>
			<td>
				near(0.005, 0.0058)<br>
				near(0.005, 0.006)<br>
				near(0.005, 0.006, 0.1)
			</td>
			<td>
				1<br>
				0<br>
				1<br>
			</td>
		</tr>
		<tr>
			<td>rad2deg(r)</td>
			<td>radian 형식의 r의 degree값을 리턴합니다.</td>
			<td>rad2deg(1.570796)</td>
			<td>90</td>
		</tr>
		<tr>
			<td>round(x)</td>
			<td>x의 반올림 값을 리턴합니다.</td>
			<td>
				round(3.1415)<br>
				round(3.7415)<br>
				round(-3.1415)<br>
				round(-3.7415)
			</td>
				<td>
				3<br>
				4<br>
				-3<br>
				-4
				</td>
		</tr>
		<tr>
			<td>sin(r)</td>
			<td>radian 형식의 r의 sine 값을 리턴합니다.</td>
			<td>sin(1.5*3.1415)</td>
			<td>-1</td>
		</tr>
		<tr>
			<td>sqr(a)</td>
			<td>a의 제곱근(square root)을 리턴합니다.</td>
			<td>
				sqr(16)<br>
				sqr(0)
			</td>
			<td>
				4<br>
				0
			</td>
		</tr>
		<tr>
			<td>tan(r)</td>
			<td>radian 형식의 r의 tangent 값을 리턴합니다.</td>
			<td>tan(3.141592/4)</td>
			<td>0.9999</td>
		</tr>
		<tr>
			<td>trunc(x)</td>
			<td>x의 소수점 이하를 버린 정수값을 리턴합니다.</td>
			<td>
				trunc(3.1415)<br>
				trunc(-3.1415)
			</td>
			<td>
				3<br>
				-3
			</td>
		</tr>
		<tr>
			<td>val_as(format, v)</td>
			<td>v값의 binary data를 format의 값으로 재해석하여 리턴합니다.<br>
			지원 format은 아래 [표 1]과 같습니다.
			</td>
			<td>
				val_as("u1", -127)<br>
				val_as("u2", -2)<br>
				val_as("s4", -2147483648)<br>
				val_as("S4", -2147483648)
			</td>
			<td>
				129<br>
				0xfffe<br>
				0x80000000<br>
				0x00000080
			</td>
		</tr>
	</tbody>
</table>


[표 1] val_as() 함수의 지원 format

<table style="text-align:left">
	<thead>
		<tr>
			<th>endian</th>
			<th>format</th>
			<th>의미</th>
		</tr>
	</thead>
	<tbody>
		<tr><td rowspan="8">little<br>endian</td>
		     <td>u1</td><td>unsigned 1 byte</td></tr>
		<tr><td>u2</td><td>unsigned 2 byte</td></tr>
		<tr><td>s1</td><td>signed 1 byte</td></tr>
		<tr><td>s2</td><td>signed 2 byte</td></tr>
		<tr><td>s4</td><td>signed 4 byte</td></tr>
		<tr><td>f4</td><td>float 4 byte</td></tr>
		<tr><td>f8</td><td>double 8 byte</td></tr>
		<tr><td rowspan="8">big<br>endian</td>
		     <td>U1</td><td>unsigned 1 byte</td></tr>
		<tr><td>U2</td><td>unsigned 2 byte</td></tr>
		<tr><td>S1</td><td>signed 1 byte</td></tr>
		<tr><td>S2</td><td>signed 2 byte</td></tr>
		<tr><td>S4</td><td>signed 4 byte</td></tr>
		<tr><td>F4</td><td>float 4 byte</td></tr>
		<tr><td>F8</td><td>double 8 byte</td></tr>
	</tbody>
</table>
