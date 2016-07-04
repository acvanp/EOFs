# EOFs
EOFs in Matlab
% Problem 3D. Using SVD calculate the EOFs of the six casts. Your data

% matrix should be constructed as NxM where N is the number of depth levels

% and M is equal to 6, the number of casts. There are six vertical (depth)

% patterns of variability. Each vertical mode will have N elements.

[c1a c1b] = polyfit(dm, c1,1);

[c2a c2b] = polyfit(dm,c2,1);

[c3a c3b] = polyfit(dm,c3,1);

[c4a c4b] = polyfit(dm,c4,1);

[c5a c5b] = polyfit(dm,c5,1);

[c6a c6b] = polyfit(dm,c6,1);

c1f = polyval(c1a, dm); % make best fit trend lines

c2f = polyval(c2a, dm);

c3f = polyval(c3a, dm);

c4f = polyval(c4a, dm);

c5f = polyval(c5a,dm);

c6f = polyval(c6a,dm);

c1dmdt = c1 - c1f; % removed the linear trends and means from the data

c2dmdt = c2 - c2f;

c3dmdt = c3 - c3f;

c4dmdt = c4 - c4f;

c5dmdt = c5 - c5f;

c6dmdt = c6 - c6f;

c1n = c1dmdt/std(c1); % normalize data variability

c2n = c2dmdt/std(c2);

c3n = c3dmdt/std(c3);

c4n = c4dmdt/std(c4);

c5n = c5dmdt/std(c5);

c6n = c6dmdt/std(c6);

DDD = [c1n, c2n, c3n, c4n, c5n, c6n];

CCC = DDD'*DDD/1221;

[eivec, eival] = eig(CCC);

for ii=1:6;

eivec(:,ii) = eivec(:,ii)/max(eivec(:,ii));

end

%What is the percentage of variance in each vertical mode?

%

% Mode 1 [0.450190753460965;] (*100%)

% Mode 2 [0.0113504284769145;]

% Mode 3 [0.00353717872773539;]

% Mode 4 [0.00189942414466527;]

% Mode 5 [0.000939472741671451;]

% Mode 6 [0.000517113315865061;]

% Problem 3E, Plot the first three vertical modes versus depth.

amps = DDD*eivec;

h = figure;

plot(amps(:, 6), dm, amps(:, 5), dm, amps(:, 4), dm)

title('Problem 3E. PC depth series for first three modes')

ylabel('depth m')

xlabel('relative amplitude')

legend('mode 1 (45%)', 'mode 2 (1.1%)', 'mode 3 (0.4%)')

set(gca,'ydir','reverse')

hgsave(h, '')

doc saveas

saveas(h, '')

% Problem 3F. Reconstruct the six XBT casts usingonly the first two

% vertical modes and their amplitudes, along with the standard deviation

% and mean.

c1r = mean(c1) + std(c1)*(amps(:,6) + amps(:,5));

c2r = mean(c2) + std(c2)*(amps(:,6) + amps(:,5));

c3r = mean(c3) + std(c3)*(amps(:,6) + amps(:,5));

c4r = mean(c4) + std(c4)*(amps(:,6) + amps(:,5));

c5r = mean(c5) + std(c5)*(amps(:,6) + amps(:,5));

c6r = mean(c6) + std(c6)*(amps(:,6) + amps(:,5));

% Plot the reconstructed casts versus depth.

h = figure;

plot(c1r, dm, c2r, dm, c3r, dm, c4r, dm, c5r, dm, c6r, dm)

set(gca,'ydir','reverse')

title('Problem 3F, Reconstructed XBT casts vs. depth from modes 1 and 2, mean

and standard deviation')

legend('cast 1', 'cast 2', 'cast 3', 'cast 4', 'cast 5', 'cast 6')

xlabel('temperature C')

ylabel('depth m')


