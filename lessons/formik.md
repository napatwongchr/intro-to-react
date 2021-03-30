# Formik

Formik คือ Library ที่จะมาช่วยเราจัดการ States ของ Form บนหน้าเว็บ

## Basic Formik

เราจะสร้าง Page Component ใหม่ที่ชื่อ SignUpPage แล้ว Link เข้ากับ Route ใหม่ที่ชื่อ Path ว่า `/signup`

จากนั้นเราจะมาลองจัดการ States ของ Form ด้วย Formik

```js
import { Formik, Field, Form } from "formik";
import { Box, Stack, Flex, Heading, Input, Button } from "@chakra-ui/react";

const MyInput = ({ field, form, ...props }) => {
  return <Input {...field} {...props} />;
};

function SignUpPage() {
  return (
    <Flex direction="column" align="center" p="10" bg="muted.200" minH="100vh">
      <Heading mb="5">Sign Up</Heading>
      <Formik
        initialValues={{
          firstName: "",
          lastName: "",
          email: "",
        }}
        onSubmit={async (values) => {
          await new Promise((r) => setTimeout(r, 500));
          alert(JSON.stringify(values, null, 2));
        }}
      >
        <Form>
          <Stack
            spacing="5"
            width="400px"
            bg="muted.300"
            p="10"
            borderRadius="2xl"
          >
            <Box>
              <label htmlFor="firstName">First Name</label>
              <Field
                id="firstName"
                name="firstName"
                placeholder="Jane"
                component={MyInput}
              />
            </Box>

            <Box>
              <label htmlFor="lastName">Last Name</label>
              <Field
                id="lastName"
                name="lastName"
                placeholder="Doe"
                component={MyInput}
              />
            </Box>

            <Box>
              <label htmlFor="email">Email</label>
              <Field
                id="email"
                name="email"
                placeholder="jane@acme.com"
                type="email"
                component={MyInput}
              />
            </Box>

            <Button type="submit">Submit</Button>
          </Stack>
        </Form>
      </Formik>
    </Flex>
  );
}

export default SignUpPage;
```
