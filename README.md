# Student-Management-System-Using-MongoDB-and-MVC-Architecture
Create a student management system using Node.js, Express.js, and MongoDB (with Mongoose). Define a Student model with properties like name, age, and course. Implement a controller to handle CRUD operations (create, read, update, delete) on student data. 
const Student = require('../models/student')

exports.createStudent = async (req, res) => {
  try {
    const student = new Student(req.body)
    const savedStudent = await student.save()
    res.status(201).json(savedStudent)
  } catch (err) {
    res.status(400).json({ error: err.message })
  }
}

exports.getAllStudents = async (req, res) => {
  try {
    const students = await Student.find()
    res.json(students)
  } catch (err) {
    res.status(500).json({ error: err.message })
  }
}

exports.getStudentById = async (req, res) => {
  try {
    const student = await Student.findById(req.params.id)
    if (!student) return res.status(404).json({ error: 'Student not found' })
    res.json(student)
  } catch (err) {
    res.status(500).json({ error: err.message })
  }
}

exports.updateStudent = async (req, res) => {
  try {
    const updatedStudent = await Student.findByIdAndUpdate(
      req.params.id,
      req.body,
      { new: true, runValidators: true }
    )
    if (!updatedStudent) return res.status(404).json({ error: 'Student not found' })
    res.json(updatedStudent)
  } catch (err) {
    res.status(400).json({ error: err.message })
  }
}

exports.deleteStudent = async (req, res) => {
  try {
    const deletedStudent = await Student.findByIdAndDelete(req.params.id)
    if (!deletedStudent) return res.status(404).json({ error: 'Student not found' })
    res.json({ message: 'Student deleted successfully' })
  } catch (err) {
    res.status(500).json({ error: err.message })
  }
}
