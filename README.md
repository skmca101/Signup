
Cypress.on("uncaught:exception", (err, runnable) => {

    return false;
})
describe('SignIn/SignUp Suits', () => {

    it('Validate Signup', () => {

        cy.visit('https://www.kapishjewels.com/');
        cy.wait(4000);
        cy.url().should('include', 'kapishjewels');
        cy.title().should('eq', 'Kapish Jewels | Online Jewellery Shopping Store India | Buy Online Gold & Diamond Jewellery');
        cy.get("div[class='header-left']>a").should('have.length', '4');
        cy.get("div[class='header-left']>a").each((ele, index, list) => {

            cy.log(ele.text());
            if (ele.text().includes("Sign In/Sign Up")) {
                cy.wrap(ele).click();
            }
        })
        cy.get("div[class='col-md-6 col-xs-5']>label>a").contains('New User?').click({ force: true });
        cy.get("input[id='first_name']").should('be.visible').type('Cypress');
        cy.get("input[id='last_name']").should('be.visible').type('User');
        cy.get("input[id='r_name']").type('cy@gmail.com');
        cy.get("input[id='mobile']").type('8888999977');
        cy.get("input[id='pass']").type('cy@123');
        cy.get("input[id='congirm_pass']").type('cy@123');
        cy.get("div[class='btn-group cart']>a").contains('Register Now').click({ force: true });

        cy.get("cy.get('#register_error')").contains('Invalid Password Format. It must be alphanumeric like Abc123')
        //cy.wait(4000);
    })

    it.only('Validate Gold Jewellery Menu', () => {
        cy.visit('https://www.kapishjewels.com/');
        //validate menu bar using mouseover
        cy.get("div[class='collapse navbar-collapse text-center']>ul").find('li').should('have.length', '76');
        cy.get("div[class='collapse navbar-collapse text-center']>ul").find('li')
            .each((ele, index, list) => {

                cy.log(ele.text());
                if (ele.text().includes('Gold Jewellery')) {
                    cy.wrap(ele).click();
                }

            })
        cy.get("div[class='col-md-6']>ul>li").should('have.length', '43');
        cy.get("div[class='col-md-6']>ul>li").each((ele, index, list) => {

            if (ele.text().includes('RING')) {
                cy.wrap(ele).click({ force: true });
            }

        })

        cy.get("#list_count").should('have.text', '160 Designs');
        cy.wait(4000)

    })

})
