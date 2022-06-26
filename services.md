import { firstNames, Geography, History, lastNames, Mathematics } from "./constants";
import { Classroom, School, Student, Teacher } from "./entities";
import { getRandomBirthDate, getRandomValueFromArray } from "./helpers";

// task 8
export function createSchoolDinamically(ammountOfClasses: number): School {
    let randomClasses: Classroom[] = []
    for (let i = 0; i < ammountOfClasses; i++) {
        randomClasses.push(createClassroom("includes", createTeacher(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), ["any_science"]), getRandomAmmountOfStudents(30)))
    }

    return {
        name: "Dinamically created school",
        address: "Minsk",
        phone: "+375 29 2330546",
        classes: randomClasses
    }
}

function getRandomAmmountOfStudents(ammount: number): Student[] {
    let students: Student[] = []
    for (let numOfStudent = 0; numOfStudent < ammount; numOfStudent++) {
        students.push(createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate()))
    }
    return students
}

export function initializeSchool(): School {
    const teacher1: Teacher = createTeacher(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), [History, Mathematics]);
    const teacher2: Teacher = createTeacher(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), [Geography]);

    const student1: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student2: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student3: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student4: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student5: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student6: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student7: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student8: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student9: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student10: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student11: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());
    const student12: Student = createStudent(getRandomValueFromArray(firstNames), getRandomValueFromArray(lastNames), getRandomBirthDate());

    const mathClass: Classroom = createClassroom("History", teacher1, [student1, student2, student12, student4, student11, student10,]);
    const geographyClass: Classroom = createClassroom("Geography", teacher2, [student5, student6, student7, student8, student12, student9]);
    const classToTestSort1: Classroom = createClassroom("Astronomy", teacher1, [student3, student6, student4, student8, student1, student9]);
    const classToTestSort2: Classroom = createClassroom("Zionet", teacher2, [student2, student6, student4, student8, student1, student9]);

    return {
        name: "Masa school",
        address: "Haifa",
        phone: "+972 4-846-4444",
        classes: [
            mathClass,
            geographyClass,
            classToTestSort1,
            classToTestSort2
        ]
    }
}
// realize the task #7
export function transferStudent(fullName: string, fromClassroom: Classroom, toClassrom: Classroom): void {
    for (let i = 0; i < fromClassroom.students.length; i++) {
        if (fromClassroom.students[i].fullName() == fullName) {
            delete fromClassroom.students[i];
            toClassrom.students.push(fromClassroom.students[i])
        }
    }
}

function createTeacher(firstName: string, lastName: string, professions: string[]): Teacher {
    return {
        firstName: firstName,
        lastName: lastName,
        professions: professions,
        fullName() {
            return `${firstName} ${lastName}`;
        }
    };
}

function createStudent(firstName: string, lastName: string, birthDate: Date): Student {
    return {
        firstName: firstName,
        lastName: lastName,
        birthDate: birthDate,
        fullName() {
            return `${firstName} ${lastName}`;
        },
        age() {
            let timeDiff = Math.abs(Date.now() - birthDate.getTime());
            let age = Math.floor((timeDiff / (1000 * 3600 * 24)) / 365.25);
            return age
        }
    };
}

function createClassroom(name: string, teacher: Teacher, students: Student[]): Classroom {
    return {
        name: name,
        teacher: teacher,
        students: students
    };
}

export function getClassYoungestStudent(classroom: Classroom): Student {
    classroom.students.sort(function (a, b) {
        return a.age() - b.age();
    })
    return classroom.students[0]
}

export function printSchool(school: School): void {
    console.log(`
School data:
============
${school.name}
${school.address}
${school.phone}\n
Classes\n==========`);

    // implementing of task 6 (2.1)
    school.classes.sort((a: Classroom, b: Classroom) => {
        if (a.name < b.name) {
            return -1;
        }
        if (a.name > b.name) {
            return 1;
        }
        return 0;
    })

    for (let i = 0; i < school.classes.length; i++) {
        console.log(`   Class ${i + 1}: ${school.classes[i].name}
Teacher: ${school.classes[i].teacher.fullName()} . Professions[${school.classes[i].teacher.professions}]\nStudents:`)

        // implementing of task 6 (2.2) 
        school.classes[i].students.sort((a: Student, b: Student) => {
            if (a.lastName < b.lastName) {
                return -1;
            }
            if (a.lastName > b.lastName) {
                return 1;
            }
            return 0;
        })
        school.classes[i].students.sort((a: Student, b: Student) => {
            if (a.firstName < b.firstName) {
                return -1;
            }
            if (a.firstName > b.firstName) {
                return 1;
            }
            return 0;
        })

        for (let j = 0; j < school.classes[i].students.length; j++) {
            console.log(`${j + 1}.${school.classes[i].students[j].fullName()} : ${school.classes[i].students[j].age()}`)
        }
    }

}
