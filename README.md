# CODEWARSIK
https://www.codewars.com/users/Deadlocki4
// 1. Two cube sums — n = a^3 + b^3 = c^3 + d^3, все a,b,c,d различны (положительные)
function hasTwoCubeSums(n) {
  const pairs = [];
  for (let a = 1; a * a * a < n; a++) {
    const rest = n - a * a * a;
    const b = Math.round(Math.cbrt(rest));
    if (b > a && b * b * b === rest) pairs.push([a, b]); 
  }

  for (let i = 0; i < pairs.length; i++)
    for (let j = i + 1; j < pairs.length; j++) {
      const s = new Set([...pairs[i], ...pairs[j]]);
      if (s.size === 4) return true;
    }
  return false;
}

// 2. IPv4 Parser

function ipv4Parser(addr, mask) {
  const a = addr.split('.').map(Number);
  const m = mask.split('.').map(Number);
  const network = a.map((x, i) => x & m[i]);
  const host = a.map((x, i) => x & (~m[i] & 255));
  return [network.join('.'), host.join('.')];
}

// 3. What century is it?

function whatCentury(year) {
  const c = Math.ceil(Number(year) / 100);
  const r100 = c % 100, r10 = c % 10;
  let suf = 'th';
  if (r100 < 11 || r100 > 13) suf = { 1: 'st', 2: 'nd', 3: 'rd' }[r10] || 'th';
  return c + suf;
}

// 4. Find the missing term in an Arithmetic Progression

function findMissing(list) {
  const d = (list[list.length - 1] - list[0]) / list.length;
  for (let i = 1; i < list.length; i++)
    if (list[i] - list[i - 1] !== d) return list[i - 1] + d;
}

// 5. Primes in numbers

function primeFactors(n) {
  let res = '';
  for (let p = 2; p * p <= n; p++) {
    let k = 0;
    while (n % p === 0) { n /= p; k++; }
    if (k) res += k > 1 ? `(${p}**${k})` : `(${p})`;
  }
  if (n > 1) res += `(${n})`;
  return res;
}

// 6. WeIrD StRiNg CaSe

function toWeirdCase(string) {
  return string.split(' ').map(w =>
    [...w].map((ch, i) => (i % 2 ? ch.toLowerCase() : ch.toUpperCase())).join('')
  ).join(' ');
}

// 7. Mexican Wave

function wave(str) {
  const res = [];
  for (let i = 0; i < str.length; i++)
    if (str[i] !== ' ') res.push(str.slice(0, i) + str[i].toUpperCase() + str.slice(i + 1));
  return res;
}

// 8. Write Number in Expanded Form

function expandedForm(num) {
  const s = String(num);
  return [...s]
    .map((d, i) => (d === '0' ? null : d + '0'.repeat(s.length - i - 1)))
    .filter(Boolean)
    .join(' + ');
}

// 9. Split Strings

function solution(str) {
  return (str.length % 2 ? str + '_' : str).match(/../g) || [];
}

// 10. Lottery Ticket

function bingo(ticket, win) {
  const wins = ticket.filter(([s, code]) => s.includes(String.fromCharCode(code))).length;
  return wins >= win ? 'Winner!' : 'Loser!';
}
