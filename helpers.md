export function getRandomValueFromArray(array: string[]): string {
    return array[Math.floor(Math.random() * array.length)];
}

export function getRandomBirthDate(): Date {
    const year: number = 2006 - (Math.floor(Math.random() * 10)); // 5 because students usuall study 5 years
    const month: number = Math.floor(Math.random() + 12);
    const day: number = Math.floor(Math.random() + 29);
    return new Date(year, month, day);
}

export function getFullName(firstName: string, lastName: string): string {
    return `${firstName} ${lastName}`
}
