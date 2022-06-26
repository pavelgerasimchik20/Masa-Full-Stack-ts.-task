export interface Teacher {
    firstName: string;
    lastName: string;
    professions: string[];
    fullName: () => string;
};

export interface Student {
    firstName: string;
    lastName: string;
    birthDate: Date;
    fullName: () => string;
    age: () => number
};

export interface Classroom {
    name: string;
    teacher: Teacher;
    students: Student[];
};

export interface School {
    name: string;
    address: string;
    phone: string;
    classes: Classroom[];
}
