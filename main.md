import { School } from "./entities";
import { transferStudent, getClassYoungestStudent, getClassYoungestStudent as getClassYoungestStudentFullName, initializeSchool, printSchool, createSchoolDinamically } from "./services";

const school: School = initializeSchool();
const newSchool: School = createSchoolDinamically(5);

printSchool(school);
//printSchool(newSchool);

console.log(`the youngest student in the class 1 is `, getClassYoungestStudent(school.classes[0]));
